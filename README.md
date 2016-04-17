[![Docker Stars](https://img.shields.io/docker/stars/evild/alpine-ruby.svg?style=flat-square)](https://hub.docker.com/r/evild/alpine-ruby/)
[![Docker Pulls](https://img.shields.io/docker/pulls/evild/alpine-ruby.svg?style=flat-square)](https://hub.docker.com/r/evild/alpine-ruby/)
[![ImageLayers Size](https://img.shields.io/imagelayers/image-size/evild/alpine-ruby/latest.svg?style=flat-square)](https://hub.docker.com/r/evild/alpine-ruby/)

# Alpine ruby

This image is based on [evild/alpine-base](https://hub.docker.com/r/evild/alpine-base/)
## What is Ruby ?

Ruby is a dynamic, reflective, object-oriented, general-purpose, open-source programming language. According to its authors, Ruby was influenced by Perl, Smalltalk, Eiffel, Ada, and Lisp. It supports multiple programming paradigms, including functional, object-oriented, and imperative. It also has a dynamic type system and automatic memory management.

> [wikipedia.org/wiki/Ruby_(programming_language)](https://en.wikipedia.org/wiki/Ruby_%28programming_language%29)

![Ruby](https://raw.githubusercontent.com/docker-library/docs/01c12653951b2fe592c1f93a13b4e289ada0e3a1/ruby/logo.png)

## Version

- `2.3.0`, `2.3` [(Dockerfile)](https://github.com/Evild67/docker-alpine-ruby/blob/c038618dd4bf76c71465f6ec323c854de66ba765/2.3/Dockerfile)
- `2.2.4`, `2.2` [(Dockerfile)](https://github.com/Evild67/docker-alpine-ruby/blob/c038618dd4bf76c71465f6ec323c854de66ba765/2.2/Dockerfile)
- `2.1.9`, `2.1` [(Dockerfile)](https://github.com/Evild67/docker-alpine-ruby/blob/03e9f3eaf49961ac482bd0eb462562f3f5809a50/2.1/Dockerfile)


## How to use this image
```
FROM evild/alpine-ruby:2.3.0
CMD ["./your-daemon-or-script.rb"]
```

Put this file in the root of your app, next to the Gemfile.

This image includes multiple ONBUILD triggers which should be all you need to bootstrap most applications. The build will COPY . /usr/src/app and RUN bundle install.

You can then build and run the Ruby image:
```
$ docker build -t my-ruby-app .
$ docker run -it --name my-running-script my-ruby-app
```
