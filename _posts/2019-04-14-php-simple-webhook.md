---
layout: post
title: PHP simple webhook
date: 2019-04-14 21:59 +0000
---

A simple php script for deploy using bitbucket webhook [^1]

[^1]: [maztch/bitbucket-webhook.php](https://gist.github.com/maztch/076198ef94402da4f70393db9352a91f)

```php
//edit with your data
$repo_dir = '~/repository.git';
$web_root_dir = '~/project';
$post_script = '~/project/scripts/post_deploy.sh';
$onbranch = 'master';
// A simple php script for deploy using bitbucket webhook
// Remember to use the correct user:group permisions and ssh keys for apache user!!
// Dirs used here must exists on server and have owner permisions to www-data
// Full path to git binary is required if git is not in your PHP user's path. Otherwise just use 'git'.
$git_bin_path = 'git';
$update = false;
$payload = json_decode( file_get_contents( 'php://input' ), true );
if(empty($payload)) {
  file_put_contents('deploy.log', date('m/d/Y h:i:s a') . " File accessed with no data\n", FILE_APPEND) or die('log fail');
  die("<img src='http://loremflickr.com/320/240' />");
}
if ( isset( $payload['push'] ) ) {
  $lastChange = $payload['push']['changes'][ count( $payload['push']['changes'] ) - 1 ]['new'];
  $branch     = isset( $lastChange['name'] ) && ! empty( $lastChange['name'] ) ? $lastChange['name'] : '';
  if($branch==$onbranch){
    $update = true;
  }
}
if ($update) {
  // Do a git checkout to the web root
  exec('cd ' . $repo_dir . ' && ' . $git_bin_path  . ' fetch');
  exec('cd ' . $repo_dir . ' && GIT_WORK_TREE=' . $web_root_dir . ' ' . $git_bin_path  . ' checkout -f');
  // Log the deployment
  $commit_hash = shell_exec('cd ' . $repo_dir . ' && ' . $git_bin_path  . ' rev-parse --short HEAD');
  //echo "Deployed branch: " .  $branch . " Commit: " . $commit_hash . "\n";
  file_put_contents('deploy.log', date('m/d/Y h:i:s a') . " Deployed branch: " .  $branch . " Commit: " . $commit_hash . "\n", FILE_APPEND);
  if(file_exists($post_script)){
    exec('chmod +x '.$post_script);
    exec('sh '.$post_script. " > /dev/null &");
  }
}
```

--- 