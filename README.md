RobotlegsJS Pixi SignalMediator Extension
===

[![GitHub license](https://img.shields.io/badge/license-MIT-green.svg)](https://github.com/RobotlegsJS/RobotlegsJS-Pixi-SignalMediator/blob/master/LICENSE)
[![Gitter chat](https://badges.gitter.im/RobotlegsJS/RobotlegsJS.svg)](https://gitter.im/RobotlegsJS/RobotlegsJS)
[![Build Status](https://secure.travis-ci.org/RobotlegsJS/RobotlegsJS-Pixi-SignalMediator.svg?branch=master)](https://travis-ci.org/RobotlegsJS/RobotlegsJS-Pixi-SignalMediator)
[![codebeat badge](https://codebeat.co/badges/f8670689-0731-4631-aa9a-5561931884ba)](https://codebeat.co/projects/github-com-robotlegsjs-robotlegsjs-pixi-signalmediator-master)
[![Test Coverage](https://codeclimate.com/github/RobotlegsJS/RobotlegsJS-Pixi-SignalMediator/badges/coverage.svg)](https://codeclimate.com/github/RobotlegsJS/RobotlegsJS-Pixi-SignalMediator/coverage)
[![npm version](https://badge.fury.io/js/%40robotlegsjs%2Fpixi-signalmediator.svg)](https://badge.fury.io/js/%40robotlegsjs%2Fpixi-signalmediator)
[![Greenkeeper badge](https://badges.greenkeeper.io/RobotlegsJS/RobotlegsJS-Pixi-SignalMediator.svg)](https://greenkeeper.io/)
[![styled with prettier](https://img.shields.io/badge/styled_with-prettier-ff69b4.svg)](https://github.com/prettier/prettier)

A port of [Robotlegs SignalMediator Extension](https://github.com/MrDodson/robotlegs-extensions-SignalMediator) to TypeScript.

Originally published on [RobotlegsJS-SignalMediator](https://github.com/cuongdd2/RobotlegsJS-SignalMediator).

Installation
---

You can get the latest release and the type definitions using [NPM](https://www.npmjs.com/):

```bash
npm install @robotlegsjs/pixi-signalmediator
```

Or using [Yarn](https://yarnpkg.com/en/):

```bash
yarn add @robotlegsjs/pixi-signalmediator
```

From version `0.2.0` of this package, the [PixiJS](https://github.com/pixijs/pixi.js) dependencies were moved to **peerDependencies**,
allowing the final user to choose the desired version of the `pixi.js` library on each project.

The `@robotlegsjs/pixi-signalmediator` package is compatible with versions between the `>=4.2.1 <5` version range of `pixi.js` library.

Since each version of `pixi.js` library defines which version of `eventemitter3` library is being used, remember to also install the proper version of `eventemitter3` in your project.

As example, when you would like to use the version `4.2.1` of `pixi.js` library, you can run:

```bash
npm install pixi.js@4.2.1 eventemitter3@^2.0.0 reflect-metadata --save
```

or

```bash
yarn add pixi.js@4.2.1 eventemitter3@^2.0.0 reflect-metadata
```

Then follow the [installation instructions](https://github.com/RobotlegsJS/RobotlegsJS/blob/master/README.md#installation) of **RobotlegsJS** library to complete the setup of your project.

**Dependencies**

+ [RobotlegsJS](https://github.com/RobotlegsJS/RobotlegsJS)
+ [RobotlegsJS-Pixi](https://github.com/RobotlegsJS/RobotlegsJS-Pixi)
+ [tslib](https://github.com/Microsoft/tslib)

**Peer Dependencies**

+ [PixiJS](https://github.com/pixijs/pixi.js)
+ [eventemitter3](https://github.com/primus/eventemitter3)
+ [reflect-metadata](https://github.com/rbuckton/reflect-metadata)

Usage
---

```typescript
import { inject, injectable } from "@robotlegsjs/core";

import { SignalMediator } from "@robotlegsjs/pixi-signalmediator";

@injectable()
export class MyUserMediator extends SignalMediator<MyUserView> {

    @inject(UserLoggedInSignal) protected userLoggedInSignal: UserLoggedInSignal;
    @inject(UserLoggedOutSignal) protected userLoggedOutSignal: UserLoggedOutSignal;

    constructor() {
        super();
    }

    private onUserLoggedIn(): void {
        // user is logged in, do something...
    }

    private onUserLoggedOut(): void {
        // user is logged out, do something...
    }

    public initialize(): void {
        this.addToSignal(this.userLoggedInSignal, this.onUserLoggedIn.bind(this));
        this.addToSignal(this.userLoggedOutSignal, this.onUserLoggedOut.bind(this));
    }

    public destroy(): void {
        // clean up memory...
    }
}
```

License
---

[MIT](LICENSE)