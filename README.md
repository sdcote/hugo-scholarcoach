
This site is using the [Airspace](https://github.com/themefisher/airspace-hugo) theme ([demo here](http://demo.themefisher.com/airspace-hugo/)) as a starting point. Refer to the [full documentation](https://documentation.themefisher.com/docs/airspace-hugo/) for details on how to use the theme.


# Deployment

First you have to create the site, then you deploy what you created:

    $ hugo -D
    $ hugo deploy

A sample run looks like this:

```
$ hugo -D
Building sites …
                   | EN
-------------------+-----
  Pages            | 59
  Paginator pages  |  2
  Non-page files   |  0
  Static files     | 47
  Processed images |  0
  Aliases          | 15
  Sitemaps         |  1
  Cleaned          |  0

Total in 571 ms

$ hugo deploy
Deploying to target "cloud" (gs://scholarcoach)
Identified 77 file(s) to upload, totaling 112 kB, and 0 file(s) to delete.
Success!
```

If you have multiple deployment targets, give the name of the deployment target, otherwise, only the first target is used:
    
    $ hugo deploy --target=<target name>

Hugo will identify and apply any local changes that need to be reflected to the remote target. You can use `--dryRun` to see the changes without applying them, or `--confirm` to be prompted before making changes.

See `hugo help deploy` for more command-line options.
    
One thing to note; Hugo creates a `public` directory in your project representing the website. It is this directory what is deployed to the cloud. Do not check this into the VCS.

# Google Cloud Platform Notes

Here are some notes for GCP.  You will probably want to authenticate with GCP first:

    $ gcloud auth login

In order for default credentials to be cached, use:
 
    $ gcloud auth application-default login
                                               
The behavior for [application default credentials](https://cloud.google.com/sdk/gcloud/reference/auth/application-default/login) has [changed](https://cloud.google.com/sdk/release_notes#12800_20160928) in `gcloud` since version 128.
                                               
You can check the version you are running and see if any updates are recommended with:

    $ gcloud --version

You can make sure your CLI is up to date with:

    $ gcloud components update

The URL to your buckets can follow the following formats:
* http://BUCKET_NAME.storage.googleapis.com/
* http://storage.googleapis.com/BUCKET_NAME/OBJECT_NAME

### Setting GCP Website Configuration

The Website Configuration feature enables you to configure a Cloud Storage bucket to behave like a static website. This means requests made via a domain-named bucket aliased using a Domain Name System "CNAME" to c.storage.googleapis.com will work like any other website, i.e., a GET to the bucket will serve the configured "main" page instead of the usual bucket listing and a GET for a non-existent object will serve the configured error page.

    $ gsutil web set -m index.html -e 404.html gs://scholarcoach
    Setting website configuration on gs://scholarcoach/...

See [docs](https://cloud.google.com/storage/docs/gsutil/commands/web) for more information.

# Adding Content




