# node-red-contrib-s3-backup
A flow designed to backup Node-Red, and store versions into S3 Buckets.

AUTO S3 Backup:

This Flow is designed to grab the working Node-Red folder, and the front end web site code located at /home/ubuntu/www, the mongo db, and zip and send the zipped content to the associated S3 bucket.

The flow depends on an external package of S3cmd, so you must install this as well.

See the contents in `INFO / INSTALL` comment node for detailed installation instructions.

After this, you will need to enter your access
key into the .s3cfg file located at /home/<username>/.s3cfg

You can generate this file by running `s3cmd --configure` in the terminal command line.


See the contents of `INFO / Install` comment node for more details on installation.





INFO / Install:

-Install s3cmd on the this host server.
`sudo apt-get install s3cmd`

run:   `s3cmd --configure`
give your credentials for the s3 bucket.


-Install zip
`sudo apt-get install zip`

When triggered, this flow will zip the contents of the .node-red folder and also the www contents in the user home folder.  Ignoring the `node_modules` folder.

Another script will utilize s3cmd to upload this file to your S3 bucket with dynamic timestamp in the file name.

The server side ~/backup-www.zip file will be static named and overwritten everytime this backup is generated... This avoids accumulations of backup files on the server.  The S3 bucket will carry all these backup variations with each timestamp attached.

There will be another S3 copy uploading the same copy to a "***-latest.zip" file for easy id of the latest backup.


