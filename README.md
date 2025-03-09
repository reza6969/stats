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

We're going to start walking through our code base right here. And we're going to point out a couple of issues inside of here. And like I said, we're going to refactor them one by one using some new typescript features.

The first thing we're going to consider is the magic string comparisons.
What do I mean by that?
The issue here is that if another engineer came and looked at our code or if you took a look at this code at some point in time in the future, you would look at this comparison right here and say match at five equals equals equals H.
What is the point of this? Like, what are we checking for right here? And so this code or this comparison is extremely unclear. And i think it would be rather challenging for other engineers to take a look at this and understand what we are trying to do.
So I think that we need to figure out some way of clarifying both these comparisons, preferably some way that remove the hard coded H and the hard coded A, because other engineers will not understand.
So to fix this up, we're going to go through a series of quick re factors. I'm going to show you a couple of different ways that we might do this comparison. And we're going to eventually settle on one way using a TypeScript feature that we have not yet seen. So here's one possible way to fix up this code.
I could wirte above my statement define two new variables.

const homeWin = 'H';
const awayWin = 'A';

There's just one issue here. Remember in that match five colume. so like this column right here, there are there are three possible values. You can have H a indicating a way and most importantly, D indicating a draw or a tie between the two teams.
So the issue here right now is that we've encoded some information about our data set into our code. If another engineer looked at these two options right here, they might be thinking, okay, the only possible outcome from a game is a how win or an away win. And we did not communicate to other engineers that there is a third possibility, which is a draw that actually could be reallly important for other engineers.
Right now, you and I are running some very specific analysis, but if we ever decided to update our code and indicate the possibility of like, you know, how many draws there are per season or something like that, we would have to know that well, I draw as a possibility and to find a draw match at five would be equal to capital D. So right now, this approach is not that great because it really just doesn't indicate the entire set of values that match at five can be.
So I think that one possible way to fix this up would be to just simply add in a new identifier here and say something like Draw is going to be capital D like so.

const draw = 'D';

So now other engineers can look at this right here and understand, okay, maybe there are three possible outcomes a home win and a way win or a draw.

But yet again, there's another issue. Notice how inside of my editor the variable draw gets faded out. That's because I declared that variable, but I never actually used it inside this file. So let me tell you exactly what would happen if another engineer came and looked at this code. They would see this annd say, oh, the variable draw is unused. Well, if it's not used, I'm just going to delete it like so. So because we don't use that variable inside of our analysis, it is incredibly likely, in my personal opinion, that another engineer would come along, delete that variable. And once again we have lost information about our data set. We no longer know that there are three possible outcomes from a match. Now we think there are only two, or at least that's what our code seems to indicate. So clearly this topic is a little bit more nuanced than you might think.
