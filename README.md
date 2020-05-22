# WF Drupal Release Action

This action builds WF Drupal projects, uploads the zipped artifacts to an AWS S3 Bucket and triggers the app deployment on the desired AWS OpsWorks Stack.

## Inputs

### `wf-webname`
**Required** The unique name of the web. Default `"example2020"`.  

### `aws-s3-bucket`
**Required** The AWS S3 Bucket Name.  

### `aws-access-key-id`
**Required** The AWS S3 Access Key ID.  

### `aws-secret-access-key`
**Required** The AWS S3 Secred Access Key.  

### `aws-region`
The AWS S3 Region. Default `"eu-west-1"`  

### `aws-opsworks-stack-id`
The AWS Opsworks Stack ID.  

### `aws-opsworks-app-id`
The AWS Opsworks App ID.  

## Example usage
```yaml
uses: wunderfarm/drupal-release-action@v1
with:
  wf-webname: 'example2020'
  aws-s3-bucket: ${{ secrets.AWS_S3_BUCKET }}
  aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
  aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
  aws-region: 'eu-west-1'
  aws-opsworks-stack-id: ${{ secrets.AWS_STACK_ID }}
  aws-opsworks-app-id: ${{ secrets.AWS_APP_ID }}
```

## Package for distribution

GitHub Actions will run the entry point from the action.yml. Packaging assembles the code into one file that can be checked in to Git, enabling fast and reliable execution and preventing the need to check in node_modules.

Actions are run from GitHub repos.  Packaging the action will create a packaged action in the dist folder.

Run package

```bash
npm run package
```

Since the packaged index.js is run from the dist folder.

```bash
git add dist
```

## Create a release branch

Users shouldn't consume the action from master since that would be latest code and actions can break compatibility between major versions.

Checkin to the v1 release branch

```bash
$ git checkout -b v1
$ git commit -a -m "v1 release"
```

```bash
$ git push origin v1
```

Your action is now published!

See the [versioning documentation](https://github.com/actions/toolkit/blob/master/docs/action-versioning.md)