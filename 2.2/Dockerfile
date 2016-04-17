FROM evild/alpine-base:2.0.0
MAINTAINER Dominique HAAS <contact@dominique-haas.fr>


ENV RUBY_MAJOR 2.2
ENV RUBY_VERSION 2.2.4
ENV RUBY_DOWNLOAD_SHA256 b6eff568b48e0fda76e5a36333175df049b204e91217aa32a65153cc0cdcb761
ENV RUBYGEMS_VERSION 2.6.3
ENV BUNDLER_VERSION 1.11.2
ENV GEM_HOME /usr/local/bundle
ENV BUNDLE_PATH="$GEM_HOME" \
	BUNDLE_BIN="$GEM_HOME/bin" \
	BUNDLE_SILENCE_ROOT_WARNING=1 \
	BUNDLE_APP_CONFIG="$GEM_HOME"
ENV PATH $BUNDLE_BIN:$PATH


RUN \
  build_pkgs="autoconf bison bzip2 bzip2-dev coreutils gcc gdbm-dev glib-dev libc-dev libxml2-dev libxslt-dev linux-headers make ncurses-dev readline-dev ruby" \
  && runtime_pkgs="bzip2 ca-certificates curl libffi-dev openssl-dev yaml-dev procps zlib-dev" \
  && apk --no-cache add ${build_pkgs} ${runtime_pkgs} \
  && mkdir -p /usr/local/etc \
	&& { \
		echo 'install: --no-document'; \
		echo 'update: --no-document'; \
	} >> /usr/local/etc/gemrc \
  && curl -fSL -o ruby.tar.gz "http://cache.ruby-lang.org/pub/ruby/$RUBY_MAJOR/ruby-$RUBY_VERSION.tar.gz" \
	&& echo "$RUBY_DOWNLOAD_SHA256 *ruby.tar.gz" | sha256sum -c - \
	&& mkdir -p /usr/src \
	&& tar -xzf ruby.tar.gz -C /usr/src \
	&& mv "/usr/src/ruby-$RUBY_VERSION" /usr/src/ruby \
	&& rm ruby.tar.gz \
	&& cd /usr/src/ruby \
	&& { echo '#define ENABLE_PATH_CHECK 0'; echo; cat file.c; } > file.c.new && mv file.c.new file.c \
	&& autoconf \
	&& ac_cv_func_isnan=yes ac_cv_func_isinf=yes \
		./configure --disable-install-doc \
	&& make -j"$(getconf _NPROCESSORS_ONLN)" \
	&& make install \
  && apk del ${build_pkgs} \
  && gem update --system $RUBYGEMS_VERSION \
	&& rm -rf /usr/src/ruby
RUN gem install bundler --version "$BUNDLER_VERSION" \
  && mkdir -p "$GEM_HOME" "$BUNDLE_BIN" \
	&& chmod 777 "$GEM_HOME" "$BUNDLE_BIN"
