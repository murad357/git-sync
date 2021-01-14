# Git Sync

A GitHub Action for syncing between two independent repositories using **force push**. 


## Features
 * Sync branches between two GitHub repositories
 * Sync branches to/from a remote repository
 * GitHub action can be triggered on a timer or on push
 * To sync with current repository, please checkout [Github Repo Sync](https://github.com/marketplace/actions/github-repo-sync)


## Usage

Always make a full backup of your repo (`git clone --mirror`) before using this action.

### GitHub Actions
```
# File: .github/workflows/repo-sync.yml

on: push
jobs:
  repo-sync:
    runs-on: ubuntu-latest
    steps:
    - name: repo-sync
      uses: wei/git-sync@v2
      with:
        source_repo: ""
        source_branch: ""
        destination_repo: ""
        destination_branch: ""
        ssh_private_key: ${{ secrets.SSH_PRIVATE_KEY }}
```
`ssh_private_key` can be omitted if using authenticated HTTPS repo clone urls like `https://username:access_token@github.com/username/repository.git`.

#### Advanced: Sync all branches

To Sync all branches from source to destination, use `source_branch: "refs/remotes/source/*"` and `destination_branch: "refs/heads/*"`. But be careful, branches with the same name including `master` will be overwritten.

#### Advanced: Sync all tags

To Sync all tags from source to destination, use `source_branch: "refs/tags/*"` and `destination_branch: "refs/tags/*"`. But be careful, tags with the same name will be overwritten.

### Docker
```
docker run --rm -e "SSH_PRIVATE_KEY=$(cat ~/.ssh/id_rsa)" $(docker build -q .) \
  $SOURCE_REPO $SOURCE_BRANCH $DESTINATION_REPO $DESTINATION_BRANCH
```

## Author
[Wei He](https://github.com/wei) _github@weispot.com_


## License
[MIT](https://wei.mit-license.org)
