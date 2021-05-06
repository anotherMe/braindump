# Docker

## Docker for windows vs Docker toolbox

//Docker for windows// is the new, full development platform, based on //Hyper-V// as the underlying driver. //Docker toolbox// is the old one, which still relies on //Virtualbox//.

Note that, once you install Hyper-V you can no longer use Virtualbox ( or maybe you can with some [[https://derekgusoff.wordpress.com/2012/09/05/run-hyper-v-and-virtualbox-on-the-same-machine/|trick]] ), so choose wisely.


### Vocabulary

**dockerfile** - used to build the //image// when you run ''%%docker build%%''

**image** - used to run your code; is an opaque asset that is compiled from the //dockerfile//



### References

[[http://blog.thoward37.me/articles/where-are-docker-images-stored|Where are Docker images stored ?]]