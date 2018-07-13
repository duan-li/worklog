---
layout: post
title: link golang to mysql via ssh
date: 2018-07-06 06:16 +0000
---

```go
package main

import (
	"database/sql"
	"fmt"
	"net"
	"os"

	"github.com/go-sql-driver/mysql"
	"golang.org/x/crypto/ssh"
	"golang.org/x/crypto/ssh/agent"
)

type ViaSSHDialer struct {
	client *ssh.Client
}

func (self *ViaSSHDialer) Dial(addr string) (net.Conn, error) {
	return self.client.Dial("tcp", addr)
}

func main() {

	sshHost := "example.com"   // SSH Server Hostname/IP
	sshPort := 22              // SSH Port
	sshUser := "ssh-user"      // SSH Username
	sshPass := "ssh-pass"      // Empty string for no password
	dbUser := "dbuser"         // DB username
	dbPass := "dbpass"         // DB Password
	dbHost := "localhost:3306" // DB Hostname/IP
	dbName := "database"       // Database name

	var agentClient agent.Agent
	// Establish a connection to the local ssh-agent
	if conn, err := net.Dial("unix", os.Getenv("SSH_AUTH_SOCK")); err == nil {
		defer conn.Close()

		// Create a new instance of the ssh agent
		agentClient = agent.NewClient(conn)
	}

	// The client configuration with configuration option to use the ssh-agent
	sshConfig := &ssh.ClientConfig{
		User: sshUser,
		Auth: []ssh.AuthMethod{},
	}

	// When the agentClient connection succeeded, add them as AuthMethod
	if agentClient != nil {
		sshConfig.Auth = append(sshConfig.Auth, ssh.PublicKeysCallback(agentClient.Signers))
	}
	// When there's a non empty password add the password AuthMethod
	if sshPass != "" {
		sshConfig.Auth = append(sshConfig.Auth, ssh.PasswordCallback(func() (string, error) {
			return sshPass, nil
		}))
	}

	// Connect to the SSH Server
	if sshcon, err := ssh.Dial("tcp", fmt.Sprintf("%s:%d", sshHost, sshPort), sshConfig); err == nil {
		defer sshcon.Close()

		// Now we register the ViaSSHDialer with the ssh connection as a parameter
		mysql.RegisterDial("mysql+tcp", (&ViaSSHDialer{sshcon}).Dial)

		// And now we can use our new driver with the regular mysql connection string tunneled through the SSH connection
		if db, err := sql.Open("mysql", fmt.Sprintf("%s:%s@mysql+tcp(%s)/%s", dbUser, dbPass, dbHost, dbName)); err == nil {

			fmt.Printf("Successfully connected to the db\n")

			if rows, err := db.Query("SELECT id, name FROM table ORDER BY id"); err == nil {
				for rows.Next() {
					var id int64
					var name string
					rows.Scan(&id, &name)
					fmt.Printf("ID: %d  Name: %s\n", id, name)
				}
				rows.Close()
			} else {
				fmt.Printf("Failure: %s", err.Error())
			}

			db.Close()

		} else {

			fmt.Printf("Failed to connect to the db: %s\n", err.Error())
		}

	}
}
```

* https://gist.github.com/vinzenz/d8e6834d9e25bbd422c14326f357cce0