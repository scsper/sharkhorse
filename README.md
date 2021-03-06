[![Sharkhorse](https://raw.githubusercontent.com/dmitriiabramov/sharkhorse/master/shark-horse.jpg)](https://raw.githubusercontent.com/dmitriiabramov/sharkhorse/master/shark-horse.jpg)
# Sharkhorse

[![Build Status](https://travis-ci.org/dmitriiabramov/sharkhorse.svg?branch=master)](https://travis-ci.org/dmitriiabramov/sharkhorse)

Test factories
```javascript
Factory.define('message', function() {
    return {
        from: 'name',
        body: this.seq(function(n) { return 'body_' + n; })
    };
});

Factory.define('conversation', function() {
    return {
        id: this.seq(),
        date: this.defer(function() { return ~~(+new Date() / 1000); }),
        messages: this.factory('message'),
    };
});

Factory.create('conversation');
// {id: 1, date: 1408118364, message: {from: 'name', body: 'body_1'}}

Factory.create('conversation', {message: {from: 'aaa', body: 'bbb'});
// {id:, 2 date: 1408118931, message: {from: 'aaa', body: 'bbb'}}


// Other functions

this.rand([min], max) // return random number from min (=0) to max
this.uuid() // generates uuid
this.factories // create many factories. `this.factories('message', 5)` will create 5 message objects
this.uniqId('seed') // => seed_{next_from_global_seq}


// TODO traits

Factory('conversation').trait('with-no-participants', function() {
    // gets merged into 'conversation' factory'
    return {
        participants: []
    };
});

Factory.create('conversation', null, {traits: 'with-no-participants'});

// TODO:
this.factories(5, 'message', {from: 'aaa'}); // => array of 5 message factories with params
this.randomString(length) // => random word/sentence/paragraph
```
