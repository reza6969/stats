# stats

11 - Reusable Code

# node 18.19.1 on my pc

# npm init -y

# tsc --init

# npm install nodemon concurrently

# npm start

we're going to figure out how to load up information out of that file using the Node.js Standard Library.
Let's take a look at the documentation for Node.js and understand how to open up and read the contents of a file.

# [nodejs.org/api](https://nodejs.org/api/)

So in the file system module we can then scroll down a pretty good amount. we are looking for a function called FS, read file sync.

# https://nodejs.org/api/fs.html#fsreadfilesyncpath-options

When we call it read File sync, it's then going to return back to us the entire contents of that file as a plain string.
And so we're going to essentially get back one big string with all of our data inside of it, like one big string with all this information.
So obviously we're probably not going to work with want to work with this information as a big string. And so that's where we're going to have to do some kind of like parsing logic or something like that to take that big string and put it into a much more usable data structure. But we'll figure out how to do that in just a little bit.
So now that we understand how to load up the contents of a file, let's flip back over to our editor and get started.

In a typical Node.js application, we can write out a required statement for the FS module without having to do any like pre
Installation step of the FS module or anything like that.

So as a quick reminder, we spoke a tittle bit ago in a previous application about type definition files. Remember, when we
work with TypeScript, we can freely work with different JavaScript libraries.
The only requirement is that we have to install something called that type definition file. The type definition files tell TypeScript about all the different objects, properties, functions, and function arguments and return values inside of these JavaScript libraries.
So any time we want to work with a third party JavaScript library, we have to install that type definition file unless it is include by default with the library itself.
So it turns out the same is true of Node.js as well.
whenever we work with Node.js from TypeScript, we have to install a type definition file.
The type definition file tells TypeScript about all the different modules inside the node standard library, all the different properties they have, all the different functions and all those functions signatures as well.
So you might think that TypeScript should ship with support for Node out of the box, or at least these type definition files. Unfortunately, no, not the case. Any time we want to make use of the node standard library, we have to install that type definition of file.
Now, one thing to point out here. Normally when we install a type definition file, we use that formula that looks something like.

# npm install @types/{name of library}

# npm install @types/fs

whenever we want to get the type definition file for any node module, like anything inside the standard library, we're always going to install these same type definition file.

Node JS Standard Lib include fs, http and os

# npm install @types/node

So, like I said, this is another issue around type definition files. The thing that is really unfortunate here is that if you recall back when we were working with type definition files before TypeScript gave us a very clear error message, it said, Hey, make sure you install a type definition file, but when we make use of a node module or anything out of the node standard library, it instead just says Hey cannot find module Fs, which is super not helpful at all. Nonetheless, that's how it works.
So just remember, any time you use a built in node standard library module, you have to install that type definition file, and that's pertty much it.

By adding on encoding Utf-8, we are telling read file sync about what type of content we expect to find inside a football csv. So by adding on this encoding flag, we are essentially telling FS read file sync to return a string to us. if we did not add on that encoding flag, it would instead give us back something called a buffer with the raw data out of that file,
which is not what we want in this case.
We just want a string representing the contents of the csv file.
