
> Everything appears to be stored inside the docker container. So doesn't that mean that restarting or upgrading the container will wipe out the data?

Hey! This is not actually an oversight, Fasten is still under heavy development, and we're not yet able to guarantee backwards compatibility between versions.

You can add a bind mount to the following directory within the Fasten container to persist the database: `/opt/fasten/db/`

So just add `-v /my/host/directory/here:/opt/fasten/db/` to the existing docker run command.

However, please note that this may cause incompatibilities between versions (and you may need to completely delete your database to fix it)

