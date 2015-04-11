# Multiple Instance Deployments #

There are certain use cases where running multiple MogileFS instances within an environment is desirable.  For example, you may want to maintain one instance in production and another elsewhere for development or testing.  The following information pertains to configuring and maintaining MogileFS in these deployments.


# Two Instance Deployment (Production/Development) #

It may be desirable to have read access to a production MogileFS instance but with write access to another instance for development and testing purposes.  In this case, a proxy can be inserted between the application and MogileFS in order to facilitate this setup.  A small python proxy program for this purpose can be found [here](http://github.com/dankosaur/moxie).