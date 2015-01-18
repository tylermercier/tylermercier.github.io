---
layout: post
title: "Learning Clojure"
date: 2013-05-27
categories: blog
---

If you are not aware of the ongoing shift from OO to functional programming, it might be worth watching this talk from Rich Hickey titled [Are We There Yet](http://www.infoq.com/presentations/Are-We-There-Yet-Rich-Hickey;jsessionid=FB30F1B231A8E7BB5917D6C235EAE2F6). It contains many solid arguments in favor of pure functional languages, like clojure.

More and more languages are including functional aspects and it definitely feels like the way programming is going. Why not take some time with clojure?

## Getting Started

The easiest way to play with clojure is with the [web REPL](http://tryclj.com/). Let's do a small experiment there now. Open the REPL in another window and copy the code below.

```clojure
(defn add [x y]
  (+ x y))
```

Now type

```clojure
(add 2 3)
```

You should see the result **5**. Congratulations, you just wrote your first clojure function. Let me explain. **defn** is a [macro](http://clojure.org/macros) for defining a clojure function. **add** is the name of the function and **[x y]** signifies that the function takes two parameters. What about **(+ x y)**? Here we are defining a clojure list literal that will take two numbers and add them together. This feels wrong at first, but if you think of **+** as simply a function invocation, it really doesn't seem that different from **add(2, 3)** which is very close to **(add 2 3)**.

Now that you have had a little taste of clojure, let's setup clojure and [leiningen](http://leiningen.org/). If you are familiar with ruby, leiningen is a magical combo of rake, bundler and rails generators. This guide assumes OSX and homebrew.

```bash
brew install clojure
brew install leiningen
```

Now to start your first project, run the following.

```bash
lein new adder
```

Here is what the project should look like.

```bash
cd adder
tree
.
├── README.md
├── doc
│   └── intro.md
├── project.clj
├── resources
├── src
│   └── adder
│       └── core.clj
└── test
    └── adder
        └── core_test.clj
```

### Project layout

The project.cli is the starting point for your application. It should look something like the following.

```clojure
(defproject adder "0.1.0-SNAPSHOT"
  :description "FIXME: write description"
  :url "http://example.com/FIXME"
  :license {:name "Eclipse Public License"
            :url "http://www.eclipse.org/legal/epl-v10.html"}
  :dependencies [[org.clojure/clojure "1.5.1"]])
```

The only part here to note for now is the dependencies. This is where you can define other libraries you code will use. Assuming we had some defined, you can run the following to include them.

```bash
lein deps
```

 Next, let's look in the src folder. The core.clj file should look like the following.

```clojure
(ns adder.core)

(defn foo
  "I don't do a whole lot."
  [x]
  (println x "Hello, World!"))
```

Let's replace that with the following. Notice our **add** function is back.

``` clojure core.cli
(ns adder.core)

(defn add [x y]
  (+ x y))

(defn -main []
  (println "2 + 3 =" (add 2 3)))
```

A few things are going on here. **ns** signifies a clojure [namespace](http://clojure.org/namespaces). In this case, we are defining our namespace.

The other new part is a declaration for main. This won't do anything just yet. We have to wire up the entry point first. Return to your project.cli file and change it to the following.

```clojure
(defproject adder "0.1.0-SNAPSHOT"
  :description "FIXME: write description"
  :main adder.core
  :url "http://example.com/FIXME"
  :license {:name "Eclipse Public License"
            :url "http://www.eclipse.org/legal/epl-v10.html"}
  :dependencies [[org.clojure/clojure "1.5.1"]])
```

Note the addition of a main symbol and our project namespace. This is what ties the projects starting point into our **-main** function.

### Running code

We should now be ready to run the actual project.

```bash
lein run
2 + 3 = 5
```

Hopefully that works. Once again, another small achievement. Your first clojure project is complete.

You can also play with your code in the [REPL](http://en.wikipedia.org/wiki/Read%E2%80%93eval%E2%80%93print_loop).

```bash
lein repl
(add 4 9)
13
```

Notice how it loaded your **add** function. This is very helpful for debugging.

### Testing

You may have noticed a test folder. Clojure has first class support for testing so let's go ahead and add our first test. Open the file located at test/adder/core_test.clj and you should see the following.

```clojure
(ns adder.core-test
  (:require [clojure.test :refer :all]
            [adder.core :refer :all]))

(deftest a-test
  (testing "FIXME, I fail."
    (is (= 0 1))))
```

Let's change that to the following.

```clojure
(ns adder.core-test
  (:require [clojure.test :refer :all]
            [adder.core :refer :all]))

(deftest addition-test
  (is (= 5 (add 3 2)) "3 added to 2 should be 5"))
```

Now when we start the tests. We should see our first passing test.

```bash
lein test

lein test adder.core-test

Ran 1 tests containing 1 assertions.
0 failures, 0 errors.
```

## Moving Forward

If you enjoyed your first taste of clojue checkout [Clojure Contrib](http://dev.clojure.org/display/doc/Clojure+Contrib+Libraries) to find some sample projects. [4Clojure](http://www.4clojure.com/) is another good site to find some clojure challenges.
