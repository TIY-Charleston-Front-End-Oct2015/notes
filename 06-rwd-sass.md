# Day 6 - RWD/Mobile & Intro to SASS

And the fun continues!

Today we covered:

- Reviewed Responsive Web with @media queries
- testing your web app/site on a mobile device using XCode, Safari inspector (iPhone), and via ip on network
- Introduction to SASS


## Installing Node.JS

### Node Version Manager

1. Install NVM - `curl https://raw.githubusercontent.com/creationix/nvm/v0.22.1/install.sh | bash
`

2. In your `.zshrc` you should see the following:
```sh
export NVM_DIR="/Users/<yourusername>/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && . "$NVM_DIR/nvm.sh"  # This loads nvm
```
This will load nvm whenever you open your shell (bash/zsh).

3. Now, in your  `.zshrc` file, add at the bottom:
```sh
# nvm
source ~/.nvm/nvm.sh
```
### Install Node

4. `nvm install stable`

5. To make sure you load the default node that you've installed, use `nvm alias default stable`

##



##

## Resources

[Using Safari on Mac to inspect mobile sites on your iPhone](http://appletoolbox.com/2014/05/use-web-inspector-debug-mobile-safari/)

[Official SASS Documentation](http://sass-lang.com/)

[SASS Guides & Tuts](http://thesassway.com/beginner)

[Modular CSS with SASS](http://thesassway.com/advanced/modular-css-an-example)


## Downloads & Installation

[Install Node via NVM](https://github.com/creationix/nvm)

[npm serve module for local web serving](https://www.npmjs.com/package/serve)

[npm node-sass module for compiling sass code](https://www.npmjs.com/package/node-sass)
