# Introduction #

CPAN is the Comprehensive Perl Archive Network.  It's accessible via the command line by executing "cpan".  As long as you have a functioning perl install (a prerequisite for MogileFS) you should have CPAN support.

MogileFS releases are uploaded to the CPAN at regular intervals, and is comprised of  several packages:

  * [MogileFS::Server](http://search.cpan.org/dist/MogileFS-Server/)
  * [MogileFS::Client](http://search.cpan.org/dist/MogileFS-Client/)
  * [MogileFS::Utils](http://search.cpan.org/dist/MogileFS-Utils/)

There are many other supportive packages, and is a good idea to [look at all of them](http://search.cpan.org/search?query=MogileFS&mode=dist).


---

# Using CPANM #

  * [App::cpanminus](http://search.cpan.org/dist/App-cpanminus/)

cpanm is a swanky way to do local builds of MogileFS. Combined with local::lib
you can pull an install into a user's homedir instead of the base OS.

You can even use it without installing cpanm:

```
$ wget -O- http://xrl.us/cpanm | perl - MogileFS::Server MogileFS::Client MogileFS::Utils
```
... will fetch cpanm, execute it, and fetch/install dependencies as well.

# Details #

The install of these modules is fairly straight forward.  If you've never ran CPAN before, you'll be guided through a simple configuration and then be ready to go.

```
$ cpan

cpan[1]> install MogileFS::Server
...
```

That's all there is to it!  Of course, if you need MogileFS::Client type that instead of MogileFS::Server.