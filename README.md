# Greenlight

![Coverage
!Status](https://coveralls.io/repos/github/bigbluebutton/greenlight/badge.svg?branch=master)
![Docker Pulls](https://img.shields.io/docker/pulls/bigbluebutton/greenlight.svg)

Greenlight is a simple front-end interface for your BigBlueButton server. At its heart, Greenlight provides a minimalistic web-based application that allows users to:

  * Signup/Login with Google, Office365, OpenID Connect, or through the application itself.
  * Manage your account settings and user preferences.
  * Create and manage your own personal rooms ([BigBlueButton](https://github.com/bigbluebutton/bigbluebutton) sessions).
  * Invite others to your room using a simple URL.
  * View recordings and share them with others.

Interested? Try Greenlight out on our [demo server](https://demo.bigbluebutton.org/gl)!

Greenlight is also completely configurable. This means you can turn on/off features to make Greenlight fit your specific use case. For more information on Greenlight and its features, see our [documentation](http://docs.bigbluebutton.org/greenlight/gl-install.html).

For a overview of how Greenlight works, checkout our Introduction to Greenlight Video:

[![GreenLight Overview](https://img.youtube.com/vi/Hso8yLzkqj8/0.jpg)](https://youtu.be/Hso8yLzkqj8)

## Installation on a BigBlueButton Server

Greenlight is designed to work on a [BigBlueButton 2.0](https://github.com/bigbluebutton/bigbluebutton) (or later) server.

For information on installing Greenlight, checkout our [Installing Greenlight on a BigBlueButton Server](http://docs.bigbluebutton.org/greenlight/gl-install.html#installing-on-a-bigbluebutton-server) documentation.

### Steps for installing BigBlueButton and installing this fork

These steps have been tested on BigBlueButton 2.3

````bash
    sudo apt-get install -y language-pack-en
    sudo update-locale LANG=en_US.UTF-8
    wget -qO- https://ubuntu.bigbluebutton.org/bbb-install.sh | bash -s -- -v bionic-23 -s bbb.nairuby.org -e benson_muite@emailplus.org -w -g
    cd greenlight/
    docker-compose down
    cd ..
    mv greenlight/ greenlight-old
    git clone https://github.com/nairuby/greenlight
    cp greenlight-old/.env greenlight
    rm -rf greenlight/db/
    cp -r greenlight-old/db/ greenlight
    cd greenlight
    ./scripts/image_build.sh bigbluebutton/nairuby release-v2
    docker-compose up -d
    cd ..
    docker exec greenlight-v2 bundle exec rake user:create["Admin","support@email.admin","AdminPassword","admin"]
    bbb-conf --restart
```

## Source Code & Contributing

Greenlight is built using Ruby on Rails. Many developers already know Rails well, and we wanted to create both a full front-end to BigBlueButton but also a reference implementation of how to fully leverage the [BigBlueButton API](http://docs.bigbluebutton.org/dev/api.html).

We invite you to build upon Greenlight and help make it better. See [Contributing to BigBlueButton](http://docs.bigbluebutton.org/support/faq.html#contributing-to-bigbluebutton).

We invite your feedback, questions, and suggests about Greenlight too. Please post them to the [Greenlight mailing list](https://groups.google.com/forum/#!forum/bigbluebutton-greenlight).

To help with organization and consistency, we have implemented a Pull Request template that must be used for all Pull Requests. This template helps ensure that the project maintainers can review all PRs in a timely manner. When creating a Pull Request, please provide as much information as possible.
