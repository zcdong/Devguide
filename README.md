# PX4 Developer Guide

[![Join the chat at https://gitter.im/PX4/Devguide](https://badges.gitter.im/PX4/Devguide.svg)](https://gitter.im/PX4/Devguide?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)

[![Build Status](https://travis-ci.org/PX4/Devguide.svg?branch=master)](https://travis-ci.org/PX4/Devguide)

This guide *is published by Travis CI* online at: http://dev.px4.io/

### Prerequisites

To start editing, install [GitBook](https://www.gitbook.com/) (requires Node.js):

On Mac OS:

```
brew install npm
```

On Linux - you're using Linux, so you should know!

```sh
sudo apt-get install npm nodejs-legacy curl
```

### Installing Gitbook

```
sudo npm install grunt-cli -g
sudo npm install gitbook-cli -g
```

Fork this repo by clicking on the FORK Button on the top right of this github site.

Git clone your fork of this repo:
```
git clone http://github.com/YOUR_GITHUB_USERNAME/Devguide.git
```

Change to the directory of this repo:

```
cd Devguide
npm install
gitbook install book

```

### Running

Build once with grunt every time the HTML template changes:

```
grunt
```

Then view it locally. *NOTE*: The local view will update when the markup files are changed,
so there is no need to re-run this command.

```
gitbook serve book
```

Open <http://localhost:4000/>. Files will update live as you edit them.

See [CONTRIBUTING.md](CONTRIBUTING.md) for information on how to submit to this guide.

## Add a new Page

To add a new page, create the "page_name".md file in the Book folder and add an appropriate location in the [SUMMARY.MD](https://github.com/PX4/Devguide/blob/master/book/SUMMARY.md) file.

## Deployment

Install required packages:

```sh
sudo gem install dotenv aws-sdk thread bundler git mime
```


```sh
export BUCKET=dev.px4.io
export AWS_KEY=[KEY]
export AWS_SECRET=[SECRET]
./deploy.rb
```

## License

Content: CC-BY, (c) PX4 Project

Template: CC-BY, stolen from the [Solo dev guide](http://dev.3dr.com).
