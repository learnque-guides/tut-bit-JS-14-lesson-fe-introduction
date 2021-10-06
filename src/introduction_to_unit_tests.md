# Introduction to unit tests

* A unit test is a way of testing a unit - the smallest piece of code that can be logically isolated in a system. In most programming languages, that is a function, a subroutine, a method or property.
* Download template project: [unit test template](https://github.com/viktornar/unit-test-template/archive/refs/heads/main.zip)

Some test examples that we will use in our tests:

```js
const car = {
    name: "Skoda",
    model: "Octavia",
    speed: {
        min: 0,
        max: 150
    },
    isPopular: true
}

export { car };
```

```js
import { car } from '../model';

describe('my car', () => {
    test('is Skoda', () => {
        expect(car.name).toEqual('Skoda');
    });

    test('is popular', () => {
        expect(car.isPopular).toBeTruthy();
    });

    test('have max speed of 150', () => {
        expect(car.speed).toBeDefined();
        expect(car.speed.max).toEqual(150);
    });
});
```

---

```js
import $ from 'jquery';

function parseJSON(user) {
    return {
        fullName: user.firstName + ' ' + user.lastName,
        loggedIn: true,
    };
}

const fetchUser = function(callback) {
    return $.ajax({
        success: user => callback(parseJSON(user)),
        type: 'GET',
        url: 'http://example.com/currentUser',
    });
}

export { fetchUser };
```

```js
jest.mock('jquery');

import $ from 'jquery';
import { fetchUser } from '../fetchUser';

beforeEach(() => jest.resetModules());

it('calls into $.ajax with the correct params', () => {
    const dummyCallback = () => {};
    fetchUser(dummyCallback);

    expect($.ajax).toBeCalledWith({
        success: expect.any(Function),
        type: 'GET',
        url: 'http://example.com/currentUser',
    });
});

it('calls the callback when $.ajax requests are finished', () => {
    const callback = jest.fn();
    fetchUser(callback);

    $.ajax.mock.calls[0 /*first call*/][0 /*first argument*/].success({
        firstName: 'Bobby',
        lastName: 'Marley',
    });

    expect(callback.mock.calls[0 /*first call*/][0 /*first arg*/]).toEqual({
        fullName: 'Bobby Marley',
        loggedIn: true,
    });
});
```

---

```js
import $ from 'jquery';
import { fetchUser } from './fetchUser';

const initDisplayUserOnClick = () => {
    $('#button').click(() => {
        fetchUser(user => {
            const loggedText = 'Logged ' + (user.loggedIn ? 'In' : 'Out');
            $('#username').text(user.fullName + ' - ' + loggedText);
        });
    });
}

export default initDisplayUserOnClick;
```

```js
// Copyright 2004-present Facebook. All Rights Reserved.

/* global document */

'use strict';

jest.mock('../fetchUser.js');

import { fetchUser } from '../fetchUser';
import $ from 'jquery';
import initDisplayUserOnClick from '../displayUser';

it('displays a user after a click', () => {
    // Set up our document body
    document.body.innerHTML =
        '<div>' +
        '  <span id="username" />' +
        '  <button id="button" />' +
        '</div>';

    // Init on click
    initDisplayUserOnClick();

    fetchUser.mockImplementation(cb => {
        cb({
            fullName: 'Johnny Cash',
            loggedIn: true,
        });
    });

    // Use jquery to emulate a click on our button
    $('#button').click();

    expect(fetchUser).toBeCalled();
    expect($('#username').text()).toEqual('Johnny Cash - Logged In');
});
```