---
title: npx versus npm
date: 2021-11-07
slug: npx-vs-npm
description: "What the `npx` command does and how it's different from `npm`"
---

You've probably used the `npm` command before and know what it does. But if you've wondered what `npx` does and how it's different from `npm`, you've come to the right place. Let's take a closer look at what `npx` is.

`npx` stands for Node Package Execute, which shipped with Node 8.2/npm 5.2.0+, and is a **task runner**.

On the other hand, `npm` is a <strong>task manager</strong>, and only installs and manages packages but doesn't run them.

Let's look at two examples to understand what this means.

---

## EXAMPLE 1

Let's say you've installed webpack (and webpack-cli) locally, by running:

```sh
$ npm i -D webpack webpack-cli
```

If you want to execute the `webpack` package now, just running the following won't work:

```sh
$ webpack
```

Why? Because it's not a global install. When executables are installed using npm packages, npm creates links to them. **Local** installs have links created at the `./node_modules/.bin/` directory. **Global** installs have links created from the `bin/` directory.

So, you have two options here:

1. Execute `webpack` using the local path by running the webpack binary:

```sh
$ ./node_modules/.bin/webpack
```

or

2. Add a script in your `package.json`:

```js
{
  ...
  "scripts": {
   "webpack": "webpack"
  },
  ...
}
```

Then run the following in your terminal:

```sh
$ npm run webpack
```

Here's where `npx` can help make things easier. After installing webpack and webpack-cli by running:

```sh
$ npm i -D webpack webpack-cli
```

you can just run the following command:

```sh
$ npx webpack
```

---

## EXAMPLE 2

Let's say, that you want to use `create-react-app`, so you run this:

```sh
$ npm i -g create-react-app && create-react-app my-app
```

And a few months later, if you want to create a new project, you need to run the following:

```sh
$ create-react-app my-new-app
```

But what if you wanted to use the latest version of CRA? You'll need to run the following command again:

```sh
$ npm i -g create-react-app
```

There must be an easier way to tackle this? You guessed it - `npx`. If you want to use the latest version of the package every time, without needing to re-install it globally, you can run the following command:

```sh
$ npx create-react-app my-app
```

---

Using our two examples above, let's look at the three main features of `npx`.

## 1. Easily run local commands

Developers used to publish most of the executable commands as global packages, in order for them to be in the path and executable immediately. But this was a pain because you couldn't really install different versions of the same command.

Running `npx <command_name>` automatically finds the correct reference of the command inside the `node_modules` folder of a project, without needing to know the exact path, and without requiring the package to be installed globally and in the user's path (see **EXAMPLE 1**).

## 2. Installation-less command execution

`npx` allows you to run commands without first installing them. This is useful because you don't need to install anything and you can run different versions of the same command, using the syntax @version.

A good example of this is create-react-app, as seen in **EXAMPLE 2** above. The different thing with `npx` here (as opposed to using `npm`) is that it will install create-react-app, run it once, then delete it — you won't have a local copy anymore.

`npx` also allows you to try out a specific package easily, without needing to install the dependencies in your local `node_modules` folder.

## 3. Run arbitrary code snippets directly from a URL

`npx` does not limit you to the packages published on the npm registry. You can run code that sits in a GitHub gist, like this one for instance:

```sh
$ npx https://gist.github.com/zkat/4bc19503fe9e9309e2bfaa2c58074d32
```

---

To summarize, `npx` is a task runner that gives you a lot of flexibility when installing npm packages, and achieving that without clogging up your machine's filesystem unnecessarily - for this reason, it's recommended you use `npx` whenever possible.

I'd love to get your feedback and comments. You can reach out to me on <a href="https://x.com/arashn_11" target="_blank" rel="noopener">X</a> or at arashnawy[at]gmail.com.
