---
layout: post
title: block chain
date: 2018-06-26 05:37 +0000
---

A blockchain includes a group of serilized blocks.
The start block is called the genesis block.



# Functions
## Blockchain
* addBlock() // push block to chain
* isValidBlock() // valify new block with latest block
* push() // add block to end of chain
* get() // return collectioin of blocks
* latest() // return last block
* generate() // return first block
* isValidNextBlock()
* isValidChain()


## Block
* `__constructe()` // default difficulty = 3
* `_get()` // magic functoin
* `hash()` // calculate hash
* `isValidHashDificulty()` // valify hash difficulty



## Mine
* `mine()` // generate new block and add to chain


## Peer

## Message

```php

interface Blockchain {
	public function get();
	public function length();
	public function last();
	<!-- public funciton genesis(); -->
	public function first();
	public function generateBlock();
}

interface BlockInterface {

}

class Block impliment BlockInterface {
	private $index; // number of block, start with 0
	private $previousHash; // previous block hash
	private $datetime;
	private $data;
	private $hash; // sha-256
	private $nonce;

	public function __construct(int $index, string $previousHash, Carbon $datetime, string $data, int $nonce)
	{
		$this->index = $index;
		$this->previousHash = $previousHash;
		$this->datetime = $datetime;
		$this->data = $data;

		$this->hash();
	}

	private hash()
	{
		$this->hash = \hash('sha256', $this->index.$this->previousHash.$this->timestamp.$this->data.$this->nonce);
	}

	private checkHashDifficulty()
	{

	}


}

const Block = require("./Block.js");

class Blockchain {
  constructor () {
    this.blockchain = [Block.genesis()];
  }

  get() {
    return this.blockchain;
  }

  get latestBlock() {
    return this.blockchain[this.blockchain.length - 1];
  }
};

module.exports = Blockchain;
```



```
isValidHashDifficulty(hash) {
    for (var i = 0; i < hash.length; i++) {
      if (hash[i] !== "0") {
        break;
      }
    }
    return i >= this.difficulty;
  }


generateNewBlock(data) {
    const newIndex = this.latestBlock.index + 1;
    const previousHash = this.latestBlock.hash;
    let timestamp = new Date().getTime();
    let nonce = 0;
    let newHash = this.calculateHash(
      newIndex,
      previousHash,
      timestamp,
      data,
      nonce
    );

    while (!this.isValidHashDifficulty(newHash)) {
      nonce = nonce + 1;
      timestamp = new Date().getTime();
      newHash = this.calculateHash(
        newIndex,
        previousHash,
        timestamp,
        data,
        nonce
      );
    }

    const newBlock = new Block(
      newIndex,
      previousBlock.hash,
      newTimestamp,
      data,
      newHash,
      nonce
    );

    return newBlock;
  }

```

# Ref
* [Demo](https://blockchaindemo.io) [GitHub](https://github.com/seanjameshan/blockchain)
* [tutorial](https://blockgeeks.com/guides/what-is-blockchain-technology/)