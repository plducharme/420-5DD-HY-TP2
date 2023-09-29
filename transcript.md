# Let’s Build a Real Time Chat Application with Elixir and Phoenix
    
    [YouTube video](https://www.youtube.com/watch?v=fyg0FuSL5DY&t=118s)
    
    2:47
    we are going to be building a **real-time chat application** uh with alien with elixir and phoenix and particularly with a module in phoenix called [live view](https://hexdocs.pm/phoenix_live_view/Phoenix.LiveView.html) which is really cool it allows like phoenix on its own was really good for real-time communication between the client and the server well and elixir itself was built for that on top of erlang so it's it's on its own really good for that but then phoenix live view takes that and takes to the next levelwhich is really cool um so we're going to be utilizing that to create some really cool stuff
    
    
    ## the first thing we need to do is we need to start a new elixir application
    4:03
    so if you guys have not done this before uh it's super easy and the cool thing about elixir is it provides some really good help even in the command line so if i just do like mix phoenix newit'll print out a whole bunch of information about the options that we have um how to configure the application interms of the generator so in this case you know this command creates a new phoenix projectand expects the path of the project as an argument a project a given path will be created and the
    4:31
    application name and module name will be retrieved from the path unless module or app is given and that
    4:37
    way we can kind of 
    
    
    specify exactly what we want things to be named it also has some options so `--live` which includes the phoenix live view module to make it easier than ever to build interactive real-time applications
    4:49
    a little plug in there for phoenix live view in the help which is pretty fun umbrella
    4:54
    which creates a number of applications so you kind of keep your business logic and um your web interface for that
    5:01
    separate um and maybe even include other interfaces in there as well uh and then the name of the otp application and the module
    5:07
    the base module and then what kind of database you're going to use um i'm going to go through a couple of
    5:13
    these first of all this dash live we are going to be creating a phoenix live view application so we'll go ahead and pass
    5:18
    this stash live it does a few things for us that makes things quite a bit easier when we're creating
    5:24
    an application um so that's nice the other thing we're going to be doing is we are going to be doing no database
    5:29
    so um the idea behind the chat application is it's going to be basically zero
    5:35
    configuration chat for the for the end user so 
    5:40
    
    
    
    
    
    you don't log in you don't even have to like manually create a room to chat in you basically just go to a url and start chatting
    5:45
    now there's some some downsides to that one is um 
    
    
    your username will be generated automatically and randomly
    5:52
    so you won't be able to choose that but um you know if you wanted to take this
    5:57
    id and run with it in a different direction you could of course allow account creations reserve
    6:02
    usernames for certain individuals that kind of thing certain accounts so but today we're just going to do
    6:07
    random usernames and go from there so no database though um no webpack so
    6:12
    that basically just says you know i'm not going to be doing this with some javascript or if i am i need
    6:17
    to manually handle it myself like move brunch or some other packaging asset building management system
    6:24
    whatever no ecto so that's what we're going to be doing we don't want to generate ecto files and ecto is a really good package to
    6:31
    help you manage your database connections and since we're going to have no database we're going to say no ecto and that's going to take care of the node
    6:37
    database stuff that we were talking about no html do not generate html views we we do want html stuff
    6:43
    git text dashboard i'll show you a little bit about phoenix live dashboard possibly once we get into it
    6:49
    it's pretty cool but we do want dashboard that's kind of fun and it doesn't really um there's no benefit to not
    6:55
    including it for us uh binary id that's primary key for ectotypes you're not going to be using ectos
    7:00
    or ecto so not not a big deal and then verbose um and then some examples down here just
    7:06
    a little more text but well let's get into it so we want to do mix phoenix new uh we're going to do live and we're
    7:12
    going to know ecto and let's call our application chat
    7:17
    super creative i know i came up with that on my own um i put a poll out i'm just kidding
    7:23
    let's just name it chat um oh no echo so it's not echo friendly
    7:29
    but we do want no ecto so it'll it created all that from our generator and we told it to go ahead and
    7:36
    install and fetch the dependencies so it's going to do that and while it's doing that
    7:43
    well let's just let that finish because it's not going to take long and the next thing to do is on the command line as well so um
    7:50
    let's talk about how we're going to generate i mentioned that we're going to be generating the uh the chat rooms names
    7:57
    dynamically or the usernames dynamically and you can essentially create a
    8:03
    chatroom on the fly and one of the things we're going to be one of the ways we're going to be able to do that
    8:08
    is by using a package called [mmonomic]( )
    8:15
    slugs man that word is so hard to say for me um but we're going to be using that to
    8:21
    um to generate some random slug information some random urls uh so that'll be nice to have um
    8:30
    from there um [Music] man this is taking a little longer than
    8:35
    i was expecting which is unfortunate but i'll tell you what let's go ahead and look [manamic slugs]( ) um
    8:40
    so let's go to github over here github and there's a cool
    8:47
    um website called [awesome elixir](https://github.com/h4cc/awesome-elixir) that i go to a lot to check out new packages or or if i'm looking for
    8:54
    something that uh that does a specific thing i can go here and find that
    8:59
    so this is [mnemonic slugs](https://github.com/devshane/mnemonic_slugs) um well search for that minomic slugs a memorable mnemonic
    9:06
    slug generator and elixir so if we look in there i'm gonna get a little give us a little bit information about how to
    9:11
    use it and um and what it is so it'll essentially you can tell it how
    9:16
    many slugs you want and it'll generate a string with that many
    9:22
    uh of those slugs in there which is pretty cool and that's how we're going to be [generating our random usernames]( ) um we're also going to allow the user to
    9:30
    if they don't can't think of their own chat room name we'll allow them just to create a random room and uh that will be
    9:38
    handled the random room name will be handled by this package as well um i think i can
    9:46
    like i'm the stream my view of the stream keeps pausing i hope it's not messing up for you
    9:53
    um so i paused it on twitch for me i'm hoping that this the chat still streams through so i can
    9:58
    see your uh questions or comments as they come in um and we'll go from there so um let's
    10:05
    check our status of our install and it's still going that is unfortunate
    10:13
    um let's go ahead and cancel that for now uh let's go into our chat um directory
    10:21
    and um let's go and start up a server and see what that looks like so we have done
    10:27
    nothing in terms of configuration of the server um let's see if it actually has
    10:33
    installed the assets and for some reason it was just hanging okay so now it's going to compile the elixir um and
    10:40
    if you didn't know elixir is a compiled language which uh makes it fast it compiles down to beam
    10:47
    the beam vm byte code and essentially it goes through
    10:53
    erlang as well and erlang is a really cool language
    10:58
    all right calib again this is taking a long time um let me check to see what is eating up
    11:04
    on my processing power and i'll be right back okay back sorry about that delay um i have
    11:11
    checked and it looks like it was potentially the my backup software this stream is also
    11:18
    being recorded to disk so the backup was just eating up the uh
    11:25
    the processing power all right so let's go to our local host and see what
    11:31
    we have here so localhost 4000 and we have phoenix it is live
    11:37
    um it is usable we can do things in it which is cool so it's got this live dashboard thing
    11:42
    um in there it shows you some stats about your running application including like uptime and your output
    11:49
    your input ports processes all this real-time information that you can get about your application
    11:55
    uh which is pretty neat but we're not going to spend a whole lot of time in there um we're going to spend most of our time out here
    12:02
    all right uh so within here um this is essentially the what the generator produces for us in
    12:08
    terms of html we don't want most of this we want to really get
    12:13
    rid of it so let's just strip all that out and go from there so let me open up the [Music]
    12:20
    the application here so it's going to be in lib chat web and from in there it's going to be under
    12:26
    templates and then layout and then root is going to be one of them
    12:33
    this is where the navigation like the header stuff is and uh let me turn off flightcheck mode
    12:40
    and um format all buffer mode uh so within here we can remove this
    12:46
    header um and we can just say i don't know h1 phoenix in action
    12:52
    chat how about that and then the inner content renders what
    12:57
    um the specific view or the specific route renders which is nice so you can see that now we have phoenix in
    13:03
    action chat let me back that out just a little bit because i think this section container has information that we're going to want so
    13:09
    let's let's do it in here phoenix and action chat let's see if that works better
    13:16
    because i kind of want that centered there we go perfect also phoenix has an auto reload mechanism so once it recognizes that
    13:23
    there's been some code changes it'll automatically reload the application uh without you having to do anything
    13:28
    and it is not um that uncommon for the um
    13:35
    for the web page to have them reloaded before i'm even able to come to the app back to the web page which is pretty crazy
    13:42
    all right so um let's check this we're going to quit that because what we're going to do next is
    13:48
    include that manaomic slugs package now that's we have things compiled so
    13:54
    that we do things um in terms of packages in the mix.exe file
    13:59
    and everything is like everything is configured here in this project function and you can see the depths
    14:05
    that's our dependencies if we go down and then it runs the depths function so if we go down here to the
    14:10
    depth function we can see these are all the dependencies that our application depends on at the moment we want to add
    14:16
    another one here of minomic slugs slugs
    14:24
    man that is so hard for me to say and spell so we're at 0.0.3 on this package
    14:31
    so we want to make sure to get that one or anything above that within the point release so we can say mixdepts.get and that'll fetch that
    14:38
    package for us and then we'll restart the server again and the next time we've restarted it
    14:43
    we'll have that package started with this so let's do mix phoenix.server and it'll
    14:50
    recompile a little bit because it's got to recompile that monomic slugs in for us um so there it is compiling
    14:56
    anomic slugs and while it's recompiling let's also
    15:01
    clear out um on our webpage here this little area right here is welcome to phoenix all that we don't need that that's not
    15:07
    something that that we need so let's clear that out and that is in um
    15:13
    a template directory template and uh since we we have we don't know this
    15:19
    yet but um phoenix when it generates the code it creates a page controller and it routes
    15:25
    uh the the root route goes to this page controller so our template is going to be um templates.page dot index or page
    15:34
    index and i'm gonna it's trying to look at every single my pat my um
    15:41
    create a git repository here because whenever i try to find a file it
    15:48
    tries to find every file in there including things like node modules and things like that so as
    15:54
    long as i create a repository it should ignore those things for me um so yeah that's gonna be a lot faster
    16:00
    so if we go to page pagelive.html.lex and look in there this is all that um that html that's
    16:09
    generating that box and that search uh thing and all that so let's get rid of this and also disable um
    16:17
    format all mode all right so we're just gonna say goodbye to this
    16:22
    save it and hopefully we've got recompiled yes so as you can see again i beat it beat me
    16:27
    to get back to the to the reload so we have nothing again which is perfect that's what we wanted we wanted nothing
    16:33
    so now we have nothing let's add something now the first thing we're going to add is just a little button to
    16:38
    allow a user to go to a random url so let's try that if we go back to our our session here
    16:45
    you'll notice i started the server with that iex capital s mix phoenix server and that
    16:50
    allows us to go into an iex reppel and if you're familiar with elixir if you're not familiar with
    16:56
    elixir iex is essentially the rebel for elixir and even though it's a compiled language it does some you know on the
    17:01
    fly compiling to and then run the code which is nice um but we can use the things that we've
    17:08
    compiled in here so if we go to monomic and then slugs and then you can even press tab and it has a lot of completion so we can say
    17:14
    generate slug and maybe like three of them and so now we have rose sahara citizen cool so that's pretty neat but
    17:22
    we want to use this on maybe like a button that would take the user to that random url um so let's create a button a button a
    17:30
    button we've got the button um so i'm just back in this blank
    17:37
    pagelive.html.lex file and um first thing we want to do is i'm just going to say a title is create a
    17:43
    random room uh and create a random
    17:49
    room and we'll see what that looks like save it there's our button right now if we click
    17:56
    on it nothing happens because we haven't added any any action to it or anything like that now phoenix provides our phoenix live
    18:02
    view specifically provides some listeners and some form handlers things like that so we can go in and
    18:09
    attach phoenix live view listeners to specific events in the browser in this case we want to listen for a click
    18:15
    on this button so we say phoenix click and when we listen when we hear that click we're going to go to the random room
    18:21
    or we're going to send the random room event to our server so now if i click it you're gonna notice
    18:27
    that my my um did you see my precursor spin just a little bit there that's because if we look in the um the logs the server
    18:35
    actually crashed the process that's running this phoenix live view that contains this phoenix live view process crashed
    18:40
    because we haven't defined a function matching in uh page live and chat web that page
    18:46
    live now you may be wondering what is page live let me go to the routes or the router file and in here you can see how phoenix
    18:54
    will handle a request to our server in this case it pipes it through this browser which
    18:59
    handles a bunch of things in terms of plugs like you know fetching the session touching flash protecting from forgery
    19:05
    that type of stuff but the thing we're interested in here is this scope here so scope slash
    19:10
    means at the root level we're going to be in the chat web um kind of namespace we're going to pipe
    19:17
    all these requests through this browser pipeline that we see above and finally within the slash we
    19:22
    anything that goes to slash from there we want to send a page live and then the index action so let's look in page live in
    19:30
    here you can see um we have a few different functions defined for us and again this was just made by the generator
    19:36
    and a lot of this we're going to we're going to delete here in a second but one thing we want to keep is this mount function every time
    19:42
    someone requests the a new web page from us um phoenix live view will run this mount action to
    19:48
    mount the page in terms of the socket the live connection to for the user so we're going to keep that
    19:54
    but this suggests search all that kind of stuff we don't want so let's just go and delete that but what we do want is to handle
    20:01
    that click so we can just say this is this impul true is basically saying yes
    20:06
    this is an implementation um we're implementing a function in this case uh so make sure that
    20:11
    it kind of basically gives you some extra error handling and messaging for that which is nice so we can say
    20:20
    def and go back to the um the error here we can kind of see how we
    20:25
    need to define this so it says the um the function that was called was
    20:32
    this page live handle event with this random room as the first argument
    20:37
    remember what we told phoenix to do when we pressed that click was to send an event named random room
    20:43
    to our server and so we need to handle that event now the second option or the second
    20:48
    parameter is a list of params and in this case there are none so we can ignore them and then finally all the events sent to
    20:56
    uh phoenix are going to be through socket connections or well the socket information and that's something we need to carry on throughout
    21:02
    the process of the connection so we're going to handle this socket as well and we'll show you how to do that in a second
    21:07
    all right so let's define that handle event random room and the first thing is first we define the function name and then another cool
    21:14
    thing about elixir if you're not familiar with it is it provides pattern matching pattern matching on your function definitions so you can have multiple
    21:20
    handle events and each one can handle a different event in this case we need to handle the random room event so
    21:26
    whenever a handle event is called where the message is sent to this process it's going to look through
    21:32
    all the handle events and find one that says okay this is the first one of the ones that are defined that
    21:37
    matches so we're going to match on random room we don't care about the parameters but we do care about the socket so like
    21:45
    in many programming languages if you uh precede a um a uh a variable with an underscore that
    21:51
    basically tells elixir that you don't really care about about what it is now if i had done this and just
    21:57
    not used it then elixir's compiler would warn us about that said hey you've got this variable that you're not using that
    22:04
    you haven't preceded with an underscore do you really want to use it and if not maybe just go ahead and pre-see that with an underscore so let's
    22:09
    do that now handle event expects a certain type of
    22:15
    return value in this case we're just going to say no reply and socket now the no reply basically means don't
    22:21
    reply to the sender of the message and in this case we don't want to reply
    22:26
    to the center of the message because that's another process we're just going to pass that straight on through and the socket is what tells um
    22:34
    tells phoenix what to do now with that socket so since phoenix basically kind of re-loops
    22:40
    on itself and handles that process and goes over and over and over and say what's the new state of the socket what's the new state of the socket what's the new state of the
    22:46
    socket and in this case we're just saying the state of the socket was the exact same as the city of the socket you gave us a
    22:51
    minute ago and we're going to change that in a minute but i'll show you what happens if we just define it like this so i'm going to save that now when i go
    22:57
    and click this we don't have that spinning cursor anymore and
    23:02
    the server doesn't crash in fact we can hear there's no crashing on the server if we wanted to we could log that out in
    23:07
    fact let's just go ahead and do that i i'm kind of a logger guy i like to just see things in my logs
    23:13
    as i'm debugging so it's likely we're going to need a logger in there anyway so in this case let's just say
    23:18
    logger info um click and save that and we can show you that indeed we are handling that click
    23:24
    event so i'll click that go back to our terminal and yes you can see in our logs now we have info
    23:30
    click perfect now what do we need to do to send the uh
    23:37
    the user on their way to a random [Music] random page random chat room well this
    23:44
    is where that manomic slugs come in comes in excuse me we can say that um
    23:50
    like a random slug equals mnemonic slugs mnemonic
    23:57
    slug generate slugs and in this case let's do maybe a four
    24:04
    string or four word slug sure why not and then let's um we can
    24:09
    just log out the slug here i'll show you that make sure that works
    24:15
    click that uh we did get a crash there let's see what that is oh no that was still reloading my bad so
    24:21
    let's try it now click it and here is our random slug we've got cactus gloria martin family
    24:27
    that's a beautiful chatroom name now we want to now redirect the user to a
    24:33
    path that has this in it that would be their chatroom path so our random slug is going to be that
    24:40
    plus the initial slash because that would be the path um so we're gonna
    24:46
    this little left uh less than greater than symbol basically means concatenate so we're concatenating the
    24:52
    string of slug sorry of the slash with the the generated slug um so now if
    24:58
    i save this well you can imagine if i click on the button now after it reloads
    25:04
    click on the button you can see that we do indeed have the slash now in front of our generated slug
    25:12
    so let us now redirect the user there now i mentioned earlier that um when we
    25:17
    return the socket it basically tells phoenix live view what to do with the connection and phoenix live view provides something
    25:23
    called a function called push redirect and it takes the socket as
    25:28
    its first argument so we're going to say for this socket push a redirect to the
    25:34
    slug so we're going to basically say go to this path now and i bet you can guess what's going to
    25:40
    happen when we save this we press the button and we'll see
    25:46
    we have an error undefont function slug now that may be because that's because i
    25:53
    didn't say random slug that's not the error that i was expecting so let's do that random slug um save
    25:59
    that and reload here oh actually i didn't even press reload again phoenix knows that uh i saved it so i reloaded for me
    26:05
    i go to random slug we can see that we were redirected to this panther silk empire special url
    26:12
    but we don't have anything that's handling that request there's no router that that handles that
    26:19
    which is something we need to define so if you're just joining us thanks for for coming in i'm jeffrey
    26:26
    lessel wrote phoenix in action for manning and um go to phoenixinaction.com
    26:31
    and if you uh put in this the code twit less 40 that's 40 off of anything i'm
    26:38
    manning not just my book but uh hopefully you pick up my book while you're there um so let me know in the chat if you have
    26:43
    any questions if we're going through this there's some contact info on the page there on the screen there as well um so uh
    26:50
    go through and and hit me up wherever you are all right let's get back to coding now
    26:58
    um we need to handle this request now we need to say now that um the request has been made we
    27:04
    need to go to the the new url uh in this case we need to go to
    27:11
    our routes our router file and um right now we're matching on this live slash basically says anytime
    27:18
    there's um any uh request for this slash page we're gonna be handled by
    27:24
    page live but instead we want to um go and um handle anything else so it's
    27:32
    basically gonna be like a wild card um it's going to catch everything else and so we can say uh within here
    27:38
    um we're going to also be a live path and we're going to use this slash and then a colon and then we're going to this is up to us
    27:44
    we're just going to name it id and let's call this room live we're going to create a module called room live to handle all this
    27:51
    and again we'll have the index action now id what that will do is anytime we
    27:56
    request something with a slash in front of it um uh anything after that it'll be
    28:03
    put into a parameter called id for us so that we can then use that to um to
    28:11
    do something we need to do later which is to subscribe to the channel's notifications
    28:17
    which we'll get into in a little bit but for now let's just do this live id room live index and again if i
    28:23
    reload here at this at this page we'll notice that we get a different
    28:29
    error now that room live is undefined so we need to create this
    28:34
    room live handler i'm going to split the page here and go back to our page live because we
    28:40
    can actually copy and paste some of this into our new module so i'm going to close that and
    28:45
    open up a new one uh oh yeah on chatweb and then live and then room live.ex
    28:52
    paste that instead of page live i'm going to change this to room live it's going to use live view we're going
    28:58
    to go ahead and put logger in there and for the mount um for now we're just going to pass this socket right on um with none of
    29:04
    these parameters and then these are signs rather and i'll talk about those a bit more later we're
    29:09
    not going to handle any events on this page yet because there are going to be no events yet and in params as i mentioned
    29:16
    now we'll have the param of id passed along and again this is where some of the pattern matching functionality and
    29:22
    elixir comes through because we can pattern match on uh the parameters that come through so we know the id is
    29:29
    going to be our room id so we'll just say the only thing we care about in the session at this point or sorry in the params at this point is the room id
    29:35
    now the session we don't care about either at the moment um and we're just going to pass the socket right on through and return okay so when
    29:41
    mount actually expects an okay if things have gone as expected when it mounts so i'm going
    29:47
    to save that and again we'll get probably a different error as it reloads here indeed it says render one was not
    29:53
    implemented for chat web room live so we need to say what do we want to
    29:58
    what we want the um the server to render when someone comes to this url so we need to define um the room live
    30:08
    dot html dot l e e x now l e e x basically means it's a live elixir
    30:13
    template um which kind of mixes up the html and the templating stuff which is pretty cool
    30:19
    so what are we going to say in our um but for now let's just say hi mom
    30:25
    and see what we get make sure oh man this is what i get for the uh the format all thing format all mode off light check off okay
    30:33
    now let's say hi mom bring back up our browser and so now we have hi mom which is neat
    30:38
    now what if we wanted to let the user know um because we're cool like that we want to
    30:45
    let them know what room they're chatting in and their username for now we don't know user names we're not going to worry about that but we are but we do know
    30:51
    already that they're at this panther silk empire special chat room um so let's let them know that that's
    30:57
    where they are so we can say uh i don't know maybe currently chatting
    31:02
    in and um we have this assign we will have this assigned we don't have it yet but we'll call it room id
    31:09
    uh and um let's do like that we'll make this strong as well strong
    31:17
    all right let's see what that looks like it's going to crash because we haven't defined the room id
    31:22
    assign um let's see did that save yeah
    31:29
    all right room id not available in the eex template so why is that what is room id so room id isn't a sign
    31:35
    if you're familiar with other web frameworks and templating things um you can it's actually the variable
    31:40
    that the controller sends on to the view in this case we don't have a controller as such
    31:46
    but we have this live view which acts kind of like a controller um as the the process so let's define
    31:53
    that room id um let's go back to our page live.eex let me split the page here again so you can see both the same time
    32:00
    so over on the right you can see our html and then on the left is uh our live view
    32:06
    function or our iphone module so when we mount we have the room id we're not doing anything with the room id at the moment
    32:12
    what we can do is we can assign to the socket um an assigned variable called room id
    32:17
    and its value is going to be what we pulled out from the function definition which is
    32:23
    room id so now if i save this um live view will will assign to the
    32:28
    socket um the variable room id and we're going to use that now in the rendering on the web page so now
    32:35
    we can say currently chatting in panther silk empire special yay uh so let's um start sliding this up
    32:42
    a little bit i am not a css person so my styles are going to be lacking
    32:48
    you're going to be able to do things much better than i would um but that is okay um okay so
    32:56
    um let's make like a chat container um because we're going to before we do it let's
    33:03
    let's make the chat container let's make it first on the page let's put it on the page um
    33:08
    so we have the currently chatting let's go ahead and add a div and name it uh chat container
    33:15
    container and in there we're gonna have uh like a messages div
    33:23
    um and there we'll say say chat goes here for now because we have no chat yet um we're just making it look the way it
    33:29
    should look and close those divs save that and let's see what it looks
    33:35
    like now so chat goes here yay so now let's make that just a little bit more
    33:40
    visible so we're going to make this display flex um to put the border on there i'll pick solid and maybe
    33:46
    something gray-ish uh how many c is that one more c sure uh yeah there we go
    33:52
    and then padding let's add in the padding in there and then margin uh we're gonna do negative one at the
    33:58
    top uh one at the right and then
    34:03
    one bottom and then negative one at the right i'm gonna put an m in here and then like
    34:11
    a flex direction uh this will be we're gonna have the uh the chat
    34:16
    input at the bottom so let's just say where the chat direction is gonna be call on here so to line it up one on top of the other
    34:21
    and uh just by the content as um space between that'll put a lot the
    34:28
    space in between the things and then let's just set the height um a solid value or a
    34:33
    static value for now and then for chat messages which is uh inside we want to grow that
    34:40
    as big as it can get and right now it'll be plenty big because we don't have anything other than chat messages so that's gonna be what it
    34:47
    looks like so we'll just put our chat in there at the bottom down here probably we'll put the um the input field uh and then on the right we'll
    34:54
    eventually put um we'll use presence phoenix presence which is really fun and it tracks user activity across your
    35:01
    distributed application which is really nice um but we'll put on like who's online who's in the channel at the moment
    35:06
    um and that'll be on the right over here somewhere uh again that'll probably look ugly but that's what we've got all right so
    35:13
    let's let's create a form for inputting chat speaking of chat let me uh look real
    35:20
    quick see if there's any chat going on um no just uh mailing this information yeah sign up for manning's mailing list
    35:25
    it's pretty cool all right so uh we're gonna do it inside this chat container for now are we yeah why not um so
    35:33
    we're gonna say f equals form four and like most uh web frameworks phoenix has some form
    35:40
    builder helpers and other functions you can use to to build forms um so form four is one of those
    35:47
    and we're going to call the form chat and for the action we're going to have it be no action at this moment
    35:53
    because we're going to do it all through phoenix live view now phoenix live view it like you may ask like what if the user has javascript
    36:00
    disabled and um in the promo videos i mentioned that we are actually not going to be writing
    36:05
    any javascript today which is insane if you think about it that um it's wild that we've got
    36:12
    this crazy real-time um interactive website this chat but we're not going to write any of the
    36:18
    javascript it's all going to be server rendered and um live view has already has the the tools in place
    36:24
    to communicate to the server and the client as needed which is pretty pretty fun
    36:31
    all right so um no but you can the reason i mentioned that is because you can fall back to an html route if you
    36:36
    need to in this case we're not going to then we're going to say this we're going to put an id of chat form on
    36:42
    here just so we can track it with our css um and then phoenix i mentioned earlier that phoenix has
    36:47
    those those hooks that they can you can log in you can hook on to to to do callbacks or handle messages to messages
    36:53
    one of those for forums is phoenix submit um and we can just say we call this one
    37:00
    submit message submit chat submit message submit message um
    37:05
    and then uh let's see do anything else in there i don't think so let's go with that then we need a text
    37:12
    input uh we'll call this the uh it's gonna be for the f variable because we're saying f is the
    37:18
    form for chat so um f and then in there it's gonna be the message and then we'll have a placeholder
    37:24
    of uh enter your message sure and then we need to close out the
    37:30
    form now phoenix does have the ability to do all this within
    37:36
    like a do block um where you don't have to manually close out the form but phoenix
    37:41
    live view the way it tracks things is um it essentially needs this f variable to be able to know when things
    37:47
    have changed uh within the the web page and render it re-render them um correctly helpfully um
    37:54
    not sure what the right word for that would be but to do it very efficiently um so we need to do it that way um so
    38:00
    now we have our chat text box here which is lovely so um i want to chat so what happens if we like
    38:07
    hit enter here and uh you know what's gonna so we see you can mention you saw that spinning
    38:13
    wheel and it crashed if go back to our logs here our server logs you can see that
    38:18
    it crashed and the reason was because we don't have a handle event submit message just like when we had that
    38:24
    um the click for the um the button to start up the um
    38:32
    or to go to the random webpage random chat room we don't have the ability to uh to
    38:37
    submit the message quite yet and i really hope the stream is coming
    38:43
    through okay i keep seeing on my presenting software that um my uh my kill bits per second goes
    38:50
    down to zero occasionally so if you're getting stutters or the stream is dropping out i really apologize i'm not sure what that is
    38:56
    um but hopefully it's fine on your end and my obs software is just lying to me because when has software
    39:03
    never lied to you all right we need to define the handle event submit message so let's do that
    39:09
    um and that's going to be inside our page live i'm sorry room live this is implementation uh so we're gonna
    39:16
    say deaf handle event and our event is submit message
    39:23
    and then it's gonna have params in this case we do care about the params because that's gonna be the forum when this submit message is
    39:30
    called or sent it's going to to grab all the information from the form and send that on with the the message so
    39:38
    we do have a chat we named the form itself chat and then within that chat form we have a field
    39:45
    called messages i'm sorry message so we can say message is we can we can um uh
    39:52
    basically pattern match that message to grab it as we define the function itself and then of course we always have the
    39:57
    socket come along as well for now let's just log out the message so log info
    40:03
    message was message and again we're going to say no reply and
    40:09
    send the socket straight on through now i think i probably have um one too few closing parentheses no
    40:17
    okay we should be good all right let's um submit a message now and see what happens a message
    40:25
    hit enter so we see it didn't crash we still have our message in the box here if we go to our terminal
    40:30
    we can see that we do have message a message so we are receiving that message fine now what do we need to do
    40:36
    with that message right we need to um uh broadcast that message
    40:41
    out to all the people who are currently subscribed to the um to the webpage i'm wondering
    40:48
    should we maybe we should do this in a different uh different order like what if we um instead of worrying about multiple
    40:55
    users first let's just worry about um well actually we can do both the same
    41:02
    time all right we're going to to do this um on mount we're going to do something
    41:08
    special here that that phoenix provides now um i mentioned that phoenix live view
    41:17
    is basically using sockets and channels to to do the communication between client and server side and um
    41:26
    it's built in already into phoenix and phoenix live view essentially builds on top of what's already provided
    41:31
    to make things really easy to configure but we're going to tap into that power ourselves and
    41:37
    um and do some of our own subscribing and and uh broadcasting things like that
    41:44
    so um the ideas the the idea of a channel is basically
    41:49
    that there's a topic and um you can subscribe to a topic and anytime
    41:55
    a message is sent out from that topic or to the subscribers of that topic then we'll need to handle
    42:00
    that message as a topic listener um so first let's define a variable or assign a variable
    42:06
    topic um and it'll say room and then um we'll append the room id to the room so
    42:15
    in this case our topic would be what was our our topic would be room colon
    42:20
    panther silk empire special um let's change this since this is just again remember we can we can put anything in here as the id so
    42:27
    if i put in just phoenix in action phoenix in action now we have a chat room dynamically
    42:32
    created for us called phoenix in action so the the channel would be named room or sorry to the topic would be named
    42:38
    room colon phoenix in action so let's do that um that's going to be a room id and um chatweb
    42:46
    defines something called the endpoint and the endpoint um within the endpoint we can subscribe to
    42:52
    topics uh so this is we're gonna say we're gonna subscribe to this topic and um our endpoint will take care of
    42:59
    all the um the leavings the goings the subscribings the the unsubscribes the message passing all
    43:06
    that's going to be handled for us um within the endpoint which is really nice um and we're also gonna
    43:11
    let's go ahead and send the topic along into our signs so that later like in other events later
    43:17
    on we can pull that topic out of the assigns and we don't have to keep um recomputing it it'll just be
    43:25
    within the socket which is nice and then um
    43:30
    let's go ahead and set up something that tracks our messages uh so let's say
    43:37
    messages um hello manning uh how about hello twitch hello twitch
    43:44
    uh so that's gonna be our messages i'm gonna put this in a list for now i'm gonna set array uh and a list for now save that
    43:52
    um and now what are we gonna do with that so we're not doing anything with the topic we're not doing anything
    43:58
    with the messages and even though we've subscribed to um the topic we haven't done anything in
    44:05
    terms of uh sending messages to that topic um but we'll do that in there in a second for
    44:10
    now let's go back to our uh our html and uh chat where it says chat goes here let's do
    44:16
    um let's actually put out the messages or list out the messages so we'll say for message
    44:21
    in messages and again we have the little at symbol because we've assigned this to the socket so
    44:27
    it's available within the view template we are going to um
    44:33
    let's say let's put it up in a p and uh put an id id there we go
    44:41
    um and the message since it's going to have it have to have an id let's let's define
    44:49
    what a message is going to look like um
    44:55
    let's not do that yet we're not going to worry about ids i'll show you why we need an id in a little bit but for now
    45:00
    we don't need it so let's not let's not complicate things so we're just going to put out the message which is just the string
    45:06
    and then let's close out our end here and close out our four all right what does that look like
    45:13
    all right so now we have hello twitch that's our first message um within uh the messages assigned so we
    45:19
    can add another one here um how are things
    45:24
    and then that should show up underneath hello twitch because we're rendering out all the messages so one of the things we want to do is
    45:30
    again i want to make this look a little bit better can we um let's not do that yet let's
    45:35
    not do that all right um instead of hello let's just
    45:40
    say something like um twitch joined the chat
    45:48
    and we'll leave it at that all right because i would like it to have um the ability to as people leave or go
    45:56
    leave or join it'll give us messages like you know geo joined the chat or richard left the chat kelly joined the
    46:03
    chat um things like that so let's keep it right there for now so now let's handle what happens if
    46:08
    someone sends a message like if i type something in here hit enter we're doing nothing the message is being received by our process
    46:15
    here in room live but it's not been doing anything except for logging it out but we want to do something more
    46:20
    so i mentioned earlier that this chat web endpoint we're subscribing to the topic right now but we're not really doing anything to
    46:26
    it for now we can say chatweb.endpoint and we could broadcast
    46:34
    to the topic so we put that in our sign so we could get it out here so socket the science topic
    46:41
    um do we name it topic yeah we named it topic in that room okay good so um the second thing um is going to be
    46:47
    the event that we're broadcasting in this case we're going to say hey a message received so a new message was sent
    46:52
    um and then the um the value or basically the payload let's
    46:59
    call the payload so the message is going to be the payload and that's again just the string for it for the moment
    47:04
    um perfect and so no reply socket's still going to be good so when we broadcast this we should see
    47:10
    something interesting uh so hello hit enter again we see the spinny blue ball and it
    47:17
    crashed look in our logs we crashed why'd we crash right without we're handling everything well
    47:23
    when we we subscribe to the topic of the room we are in and then we send a message to that topic
    47:28
    but we haven't handled that message um and messages uh like this these broadcast messages
    47:34
    are handled within handle info function so we need to find this handle info with this event information in it as well that
    47:41
    should be too hard so we'll imple true def handle info and we can pattern match
    47:48
    on the message which was a new message no sorry the event not message message on my mind
    47:56
    new message and you can see the next thing within this um struct of the phoenix socket broadcast the next thing was
    48:02
    payload which was which had the message in it so payload the payload key has our message
    48:09
    what else do we need from there we have the topic of the room topic which we don't need in this situation um and
    48:15
    then we have the socket itself which of course we are going to need so let's take the socket
    48:22
    and do something in here so we can say let's just log this out again um let's say payload this time to
    48:28
    make it a little bit different than the other and again we're not going to reply but we are going to pass the socket on as it was all right so now when we
    48:37
    submit a message we should see a logger info here for message of the message and then
    48:43
    it's going to broadcast that out to all the the listeners the subscribers to the topic which we
    48:48
    are one so we should see another info of payload with that same message let's see if that's what we actually get
    48:54
    uh do you hear me
    48:59
    all right looks like something happened yes we have message do you hear me and payload do you hear me perfect that is
    49:06
    what we wanted um so we have that now so what do we do with it well we can
    49:12
    append that to the list of messages and then phoenix is smart enough to know that
    49:19
    that messages has changed so it will then re-render all it reads
    49:24
    to render um to um
    49:30
    to make the page work i can't think of a better way to say it it makes the page work um so
    49:36
    how are we gonna do that for now right now okay remember we're looping through we're iterating through the messages
    49:42
    um and so we want to append that to the list of messages so let's do that um so instead of log or just logging yet
    49:49
    we're going to assign this to the socket um our messages and
    49:54
    in this case we're going to say the socket assign so what's in messages right now
    50:00
    um and then tack onto that the new message
    50:06
    all right so this little i call it the um the guillotine operator it's
    50:13
    it's not the name of it but i like to think of it like that because it separates the head from the tail so this basically says
    50:19
    pull the messages in there first and then also the the new message um although this isn't gonna work quite
    50:25
    right so let's do something a little different let's instead of this way let's just do this appending there
    50:32
    like that that'll tackle on to the end all right so let's say did you get
    50:40
    this okay so it's nothing something something did go wrong um key message
    50:46
    not found in oh because it's messages yeah so messages on this one
    50:54
    plus the new message all right that'll reload um hello all right so now we have hello
    51:01
    showing up on our messages because again phoenix tracks the state of
    51:06
    the signs in the slot in the socket recognizes that there has been a change in the messages assigned
    51:12
    and then re-renders just that part of the html in fact if we look at the um
    51:21
    at the network requests let's see um let's do another one another
    51:28
    oh you know what i need to reload to get this websocket connection and i think it might be this one
    51:34
    response okay so if we say hello so it sent that um request response
    51:42
    that's just maybe is this one yeah here we go
    51:51
    uh yeah so you can see that uh in this message it did send both of our messages
    51:56
    because that is the messages assigned it also has this form um because we're not doing things super efficiently with the form but that's
    52:02
    okay for what we're doing today uh so again all it sent was this hello which is super nice well and this twitch during the chat but we're gonna
    52:09
    you may be thinking well what if you have like a million messages and every time what you're doing is you're appending
    52:14
    the new message to the list of a million messages that's not going to scale well and you are correct good for you you get the
    52:20
    gold star but instead we want to do something well phoenix already thought of that too
    52:26
    so um the way that phoenix thought of that is it's like well this is going to happen we need a way to
    52:32
    deal with that because it stores the assigns in a process and that process is long running so that's still going on
    52:38
    on my server it's just keeping track of this process as my my browser is connected
    52:47
    oh another very important thing about our chat application that i forgot to mention that's going to come into play here is
    52:53
    if you're not there when the chat is sent then you don't see that message so it's not like slack where it's got
    52:59
    the history there is no history that's why there's no database there's no users it's like it's like if the tree falls in
    53:05
    the force no one's around to hear it it doesn't make a sound in this case it makes no sound um there's no one to hear it it's like it
    53:12
    never existed it's ephemeral it's gone it's never it was like it's never gone never there in the first place
    53:18
    so um phoenix handles this through something called temporary assigns temporary assigns so
    53:25
    in here we can tell it which assigns we're considering temporary in this case messages is temporary
    53:31
    and once it uses the value of messages we have to tell it what to basically
    53:36
    reset that value back to so in this case we want it back to an empty array sorry empty list let me save that should reformat a
    53:42
    little bit better there we go um so what's it going to do so phoenix is going to take
    53:48
    the initial value of messages here which is going to have which has you know twitch join the chat it's going to go to our html and iterate
    53:54
    through all our messages and uh print out the message in our little p tag here
    53:59
    and once it's done doing that it knows hey i've done what i need to do with this message is assigned so i'm going to then
    54:06
    throw it away basically i'm going to reset it to this temporary state of messages equals an empty array
    54:12
    now if you think about it you're like well we have to now if i type in hello um
    54:19
    well that still comes through because we have the size messages did that save maybe i didn't save that
    54:26
    let's try it oh i did save it hello okay well didn't do what i thought
    54:34
    i was going to do which i thought was going to erase everything in the messages because now we only have that one
    54:40
    message but um now we want to when it receives a new
    54:46
    message to um just put that new message into the into the list of messages because that's the only
    54:53
    one that we now care about so in here
    54:59
    if we do that now hello you can see that it takes the place of the previous message
    55:06
    and that's not what we want either um but again phoenix has thought of that so within this chat messages it has this
    55:12
    phoenix update callback or attribute and it says whenever phoenix receives an
    55:19
    update for this div what do we do with it now the default is replaced so it'll just replace that whole div with the new
    55:25
    information um and and go from there but instead of replace we want to append
    55:32
    that's another option for phoenix update plus a pre-pin and a couple others that are all covered in the documentation
    55:37
    which is excellent by the way uh someone to append that means just pop it at the end of the whatever list you already had going
    55:43
    um and that should be good so hello um that did not do it either
    55:50
    so let's see here we do have our message hello um and
    55:57
    i'm not sure why we don't have the list of messages anymore
    56:05
    because we're going to sprinkle message let me just make sure we're still getting this payload a message
    56:17
    all right send a message here and yeah we are getting the payload okay
    56:25
    interesting so let's figure this out why is this uh coming through in this manner um what
    56:31
    we can do is we can actually log out the the current state of messages also it's interesting that
    56:39
    for now the um the message is like when i reload the
    56:46
    page so if i read the page you can see that this says twitch during the chat but it goes away real quick
    56:51
    i don't know if you can see that uh through the stream but reload it's there and it's gone so we gotta figure out why that is um
    56:58
    because that should not that should not be happening either um so let's
    57:04
    think about this it might be that i put in the wrong um phoenix update
    57:12
    tell you what let's go to those excellent docs i was mentioning and check it out so let me see dash
    57:21
    and then uh nothing here but we want uh there's a guide for handling form
    57:27
    bindings in here so um uh you know what that is phoenix change
    57:34
    for events no we don't want form events we just want uh regular binding so go back to the live view docs so phoenix
    57:42
    live view and then down here we can see bindings all right so we have
    57:50
    click events form events focus blend events key events uh which is cool to handle
    57:55
    like uh keyboard shortcuts which is pretty neat uh former events form or phoenix change
    58:00
    but dom patching is phoenix update um so i think we should have uh
    58:05
    we did have it right phoenix update i'm wondering if i put it in the wrong dom so we have replace ignore append and
    58:13
    prepend um and this might be
    58:19
    where the the id thing i was talking about earlier might come into play uh it goes through and talks about how
    58:24
    you know we do have temporary signs oh it's got messages as well um and
    58:29
    uh let's see now whenever there are more than one or more new messages we'll sign only the new messages to messages um
    58:36
    in the template we wrap went to wrap all the messages in a container and tag this content with phoenix update
    58:41
    remember we must add an id to the container as well as to each child so that's the reason
    58:47
    it's not coming through is because we're not attaching an id to the child
    58:52
    and i should have added it earlier i know he's going to get into the trouble but for now let's just say it's the message itself so the id
    58:58
    is the string of the message which as you can imagine will also get some trouble later because what if you put in the same
    59:03
    message twice but now at least we'll be able to see hello be appended to our list of messages and we know that
    59:09
    um uh thanks from um yes there's the uh if
    59:16
    connected he mentioned that or um thump mentioned that there is an if connected uh thing you can do so you can
    59:23
    say if connected socket that we can do some things uh do you know hi um but for now
    59:28
    we don't need to do that we can if we wanted within the subscribe so um
    59:35
    so if connected instead of socket then we can do this subscribe subscribe to the topic
    59:43
    but in this case the issue was the id um oh if connected
    59:53
    there we go okay back to being good um now we need to do something a little better than just handling the id as the
    1:00:00
    message itself so um there's another package that we can use called uh uuid that's just like
    1:00:06
    simple let's just generate something completely random um 1.8 is the current thing so again we
    1:00:13
    need to reshape the server because we're going to break it install those dependencies dips.gip and
    1:00:21
    that's done so let's restart the server it's going to compile those things
    1:00:27
    there's a few warnings within the uid package itself but we don't really care about those at the moment so now we're going to start talking
    1:00:33
    about um handling the message in a in some sort of structure because right now it's just the string but we're
    1:00:39
    going to need some more information about it like that uuid so what can we do we can do a few
    1:00:45
    different things we can create its own module we can that would basically be its own struct that would might be
    1:00:52
    the smarter thing long term short term let's do something um a little
    1:00:59
    faster so we can just say uid and uid has a i think it's uuid for function we'll
    1:01:05
    see if that blows up actually let's check it in the iex session uid uid4
    1:01:11
    yeah cool that gives us the id so we're gonna have this random id um and then uh in the uid key within our
    1:01:19
    map here and then we'll have maybe just like the maybe content
    1:01:25
    content yeah this is called content content um and let's do that save that
    1:01:33
    now it's going to blow up because in our html we have we're not handling um into that map we're just saying that
    1:01:39
    we're just handling if it was a string so we do need to handle it as a as the map so for each message now the
    1:01:47
    id is going to be the message uid and uh the the printed content is going to be message
    1:01:53
    content save that uh we should now get messages
    1:01:58
    again but again if i um type a message we'll we'll crash again because we're
    1:02:04
    not handling the correct message type in this handle event let me kill out these loggers and instead of a
    1:02:11
    new message with just passing on the string we can say the message is going to be this map here and again we're going to
    1:02:17
    need a uid uh duid4
    1:02:24
    and then the content is going to be the message which again is the string that we're receiving from the form
    1:02:30
    so we're going to pass that on as the message or broadcast that as the message uh so now
    1:02:37
    everything's hooked up correctly again and now we have the uuid uh handled as well which is nice let me
    1:02:43
    make this a little bit bigger there we go no reason to waste that screen space that sweet sweet screen space
    1:02:53
    all right thank you for um for going through that with me that was quite the journey but we did it all right what's next
    1:03:01
    what if um each user that comes in like right now i can type hello um oh by the way let me bring up another
    1:03:09
    page here the browser window and show you that this is already
    1:03:15
    handling multiple connections localhost 4000. oh yeah and we wanted to go to the
    1:03:21
    phoenix inaction chat room because that's where all the action is happening uh i'm here too
    1:03:28
    sweet so you can see that i entered it here um and we got it on the initial uh browser
    1:03:34
    which is what we wanted you can also see that as i mentioned this hello was sent during this
    1:03:40
    session's lifetime but not during this session's lifetime so this session on the right has no clue that that happened
    1:03:45
    earlier which is kind of what we want we want to be like if you're not here for the party then you don't get to see what happened
    1:03:51
    uh let me just uh keep this over to the side i don't know how that's going to look
    1:03:57
    but sure let's try that one big one small
    1:04:02
    now another thing you may mention is or you may see is as i'm you know entering messages here
    1:04:08
    that the um content that text area content or text input
    1:04:15
    content doesn't change doesn't go away there's a few different things we can do to handle that um and i originally
    1:04:20
    planned on handling that later but it's just gonna annoy me that it doesn't go away so let's handle it now right
    1:04:27
    this is the again the two different ways we could do it um that i could think of there's probably others is we can actually write a javascript
    1:04:34
    hook um that will listen for events and um and clear out this input as uh
    1:04:41
    as it's submitted um again i really wanted to do this whole thing without writing any javascript so we're
    1:04:46
    not gonna do it that way instead we're going to hook into another um
    1:04:51
    another hook that phoenix provides so again or if you remember we had this in this form we had this phoenix submit
    1:04:56
    submit message but we also can have phoenix update and that means every time any
    1:05:02
    and every time anything in this form changes uh send this message to the process the handling process um
    1:05:08
    so we can say uh i don't know form updated
    1:05:14
    all right so then we need to handle that right um so we have the submit message event handled uh so implementation true
    1:05:21
    handle events uh what did i call it form update
    1:05:27
    let's not say update and say update now what do we want to do on the update um again we have the chat form and
    1:05:33
    within there we have the messages text field and we can call that message
    1:05:41
    and then the socket of course always and
    1:05:49
    we can basically track the value of that form so let me show you let's again
    1:05:54
    let's log out here uh the message message and we don't do a no reply
    1:06:02
    and just pass on the socket as it is so nothing's gonna happen in here except for locking it out
    1:06:07
    so now um let me see if i can uh what's the best way to do this i'll
    1:06:13
    go this up a little bit all right so now when i type a message every time i type a
    1:06:19
    letter we should see something going on the logs and we don't perfect are we getting that
    1:06:26
    message probably not because we're not logging that info out
    1:06:32
    um save that reload all right is it form update or phoenix
    1:06:38
    update no it's phoenix change i think it was yeah not a phoenix update it's phoenix
    1:06:44
    change all right let's try it out
    1:06:51
    if you're like familiar with phoenix you're probably shaking your fist at me right now um all right what we have a crash here
    1:06:58
    why is that because we're not handling the event correctly we have form update uh the csr token we don't care about
    1:07:04
    that oh chat message and then that so what are we not um handling correctly it
    1:07:09
    must be something in here that i'm doing uh oh i'll do messages so again
    1:07:16
    i mentioned that elixir does pattern matching on the um on the functions so in this case
    1:07:22
    it tried to match the complete pattern we gave it which was chat and within the chat map there's a messages key
    1:07:28
    and within the messages key there's a message value but there is no messages key it's called message uh so let's try it
    1:07:35
    now all right so we have the log down below and as we type yeah you can see that the message continues to build as we type
    1:07:42
    and that's what we want because then what we can do is um when
    1:07:49
    we submit the message the chat message we can reset this assign we can assign first of all
    1:07:54
    we need to make an assign so we can assign the message string so you can say message equals blank
    1:08:00
    and in here we have this text input message and it actually uses the value
    1:08:06
    of the assigns in this case it's going to be message which is going to be helpful for us it could be confusing if you didn't know that that's happening
    1:08:13
    but that's uh that's what we're going to do and so then we can say form update message
    1:08:19
    message we're going to assign to the socket message is going to be
    1:08:27
    the current con the current value of what's in the message text field and then over the text input we need to
    1:08:34
    tell it that uh what the value of it is so again let me look in the documentation
    1:08:39
    for text input see which one that is text input here
    1:08:46
    we have form field options um see the form should either be a form
    1:08:52
    emitted by form 4 or an atom all given options are 4 to 2 to the underlying input default values provided for id
    1:08:57
    name and value if possible so let's try value so placeholders forwarded on and
    1:09:03
    value also be forwarded on so value equals message
    1:09:12
    all right let's see what that does hello um and then
    1:09:19
    uh let's do form submit so when we submit the message we also um right now we're just passing the
    1:09:24
    socket on but instead we want to reset the message assign to a blank string
    1:09:29
    now let's cross our fingers and see if this works hello yeah okay perfect
    1:09:38
    so basically um it's if you're familiar with react it's kind of like a controlled input now
    1:09:43
    um to where we're telling it what the value is it just happens to be that whatever we type is going to the server
    1:09:48
    setting and assign the assign is going back to our view and saying this is now your value as an input
    1:09:54
    um the javascript way probably is the the faster a better way but again i wanted to do this stream without writing
    1:09:59
    any javascript just to say we could do that so sweet now we need users
    1:10:06
    okay let's generate some users
    1:10:14
    to do that um let's generate a user so the user is
    1:10:19
    going to be the mnemonic slugs again and we can say
    1:10:30
    generate slug not generated slug generate slug let's just say two
    1:10:36
    um and the username is going to be the username so let's change this from user to
    1:10:42
    username um
    1:10:48
    so let's say instead of twitch around the chat let's say username join the chat and see if that works i think generates i think i got the the
    1:10:54
    manaomic slugs thing right yeah so in this case i am agent deliver oh that's pretty sweet name
    1:11:00
    um and over here on the right is tripod history um so since the user's not picking their
    1:11:06
    username let's let them know who they're chatting at so up here in our top right we see the html of what's
    1:11:12
    being generated um so we're saying currently chatting in the room id and then we can say like i don't know as
    1:11:19
    like the strong again and then the username close out that strong
    1:11:28
    all right and find function username because i didn't put a ampersand or like a symbol in front of
    1:11:33
    that it's not a local variable alright so now we are currently chatting in phoenix in
    1:11:38
    action as child arctic sweet and on the right it's screen arrow
    1:11:44
    alright so charlotte child architect joined the chat and screen arrow join the chat those again if you remember those are
    1:11:51
    just statically generated based on the current user who they are at the moment um but we need to do
    1:11:56
    something a little more uh dynamic let's say because if like if
    1:12:03
    another person joins like if we go and join again um all right we want the
    1:12:08
    phoenix in action chat room phoenix in action
    1:12:14
    uh so phoenix dispute joined the chat but these two you know screen arrow and child arc arctic doesn't don't know about phoenix
    1:12:20
    dispute yet wow phoenix how strange that phoenix came up as a random name that's pretty fun
    1:12:26
    all right bye phoenix defeat dispute um so we want to be able to track those as well so how do we do that um let's do that
    1:12:33
    through presence let's get into presents um
    1:12:42
    no let's not get into presence yet but instead let's check let's um track who uh submitted the message
    1:12:48
    so if i press sdf i know i typed that but over here in a screen arrow's screen he doesn't know
    1:12:54
    that child arctic is the one who typed that so that's one more piece of metadata we
    1:13:00
    need to track within our assign or sorry our map here that's checking the message contents
    1:13:05
    so we have uuid we have the content let's also put the username in here
    1:13:12
    for now let's just say username system for this initial message but eventually this mess
    1:13:18
    this initial message is going to go away but for now let's just say that because it's going to need something um and so for this message the username
    1:13:25
    is in our socket so we can say socket assigns uh username and it's going to broadcast
    1:13:31
    that message and it's going to pass that on to the view template uh and we can handle it there so instead
    1:13:38
    of just message content let's say um the username
    1:13:44
    type in the username put out the username oh it's the message username right not
    1:13:50
    the assigns username it's the message username close out that strong and then a colon
    1:13:56
    and then the message content all right so now we have system row scorpio join the chat so if i
    1:14:02
    enter a message over here as rose scorpio then press sample over here on the right should see that this message
    1:14:07
    is for me or from me um hi i'm rose sweet so now we have
    1:14:15
    um we know who is actually sending this message so press sample um hi
    1:14:21
    rose uh i'm sample
    1:14:28
    cool now both know who each other what what they're talking about um if
    1:14:34
    you're if you've not joined us for a little while thanks for for joining in uh midway my name is jeffrey lessel i wrote phoenix in action
    1:14:40
    let me just go through this again i want a few places online um twitter is at geolessel and then i've
    1:14:46
    got a blog at jeffreylessel.com i haven't done anything with it for a while but there's still some good content up there
    1:14:52
    about ecto and elixir uh and then i do some youtube streaming as well um at
    1:14:58
    youtube.com c geolessel i've been doing some um emacs stuff
    1:15:03
    recently uh but i'm hoping to do more elixir stuff on there as well soon so join me there also if you're watching
    1:15:09
    and you want anything from manning.com uh at 40 off then today's your lucky day because you can just type in twit
    1:15:15
    less 40 to get 40 off everything at manning.com including phoenix in action let me show
    1:15:21
    you this if you go i made it really easy i put up a read act if you just go to phoenix in action
    1:15:26
    uh if i spell it right phoenix inaction.com it'll take you right there
    1:15:31
    it'll take you right to manning's page add it to your cart enter twit less 40 to get 40
    1:15:36
    off and if you go to this particular url i'll just get a little bit more for it um and that will help me out i
    1:15:43
    really appreciate it um so thank you for doing that let me go back to
    1:15:49
    uh coding let's get back to it thanks for allowing me to do that and thanks for showing up by the way i really i
    1:15:54
    really do appreciate it it's kind of fun being here again if you have any questions or anything like that you want to see something specific put it in chat
    1:16:00
    um i i did find a way to pop out that chat so i don't have to do watch the stream and stream at the
    1:16:06
    same time because that was you know my eyes are starting to water doing that but i can't see your chat so
    1:16:12
    that's good all right so we have the ability to track who sent the message um and print that out on anyone who
    1:16:18
    subscribed to this page or who's logged into the page or not logged in but who's open to this page because they are subscribed to that
    1:16:24
    topic now let's get into tracking um
    1:16:30
    presence because that's pretty fun when i first saw how easy presence was in phoenix my mind was kind of blown um
    1:16:38
    and because i'm like that i'm just going to pull out this form into the out here because
    1:16:45
    i didn't like the way it looked inside inside there so that doesn't look any better it looks
    1:16:51
    pretty nasty but yeah it looks well maybe it looks better let's say it looks better let's pretend you and i let's pretend let's play
    1:16:57
    pretend that that is better it actually will look better when we put in um
    1:17:04
    the uh the box for the users so let's build that box just to make it look better for now so
    1:17:10
    um in here let's say div id equals uh user list maybe um
    1:17:18
    and then for now let's just say you know user one and user two
    1:17:25
    let's do that and click the div and uh let's see what that looks like we're going to do some css because remember we did this as
    1:17:33
    a flex column i believe it was let me go back
    1:17:39
    to my css app css uh yeah flex direction
    1:17:44
    column so let's delete that this should put it side by side it does which is good um
    1:17:50
    let's put the border on chat messages uh so then we need the margin on chat
    1:17:59
    messages too there we go so the users are on the on the right um
    1:18:07
    and let's uh put in like a h2 like an h3 users online
    1:18:18
    yeah again this isn't a css session as you can plainly see
    1:18:25
    but we'll say this is good enough for us all right um i did lose some of my my padding um
    1:18:31
    inside my chat messages which i do like let's do that all right cool
    1:18:37
    boom hire me as your next designer okay moving on let's do presents
    1:18:43
    what is presence presence is something built into phoenix that uses um
    1:18:50
    i forgot the the acronym i guess let's go to presents here in the docs which again are
    1:18:55
    excellent uh phoenix presents it does it with um
    1:19:04
    oh shoot i forgot it was called it's not in here i thought i mentioned the the crazy word it used to uh to do the presence
    1:19:11
    over multiple servers but anyway it was just some protocol to handle
    1:19:16
    um distributed uh presence tracking so that when a user logs in
    1:19:22
    that user is tracked not tracked in the sense of like we want to know where they're going so we can sell them ads
    1:19:27
    but more like is this user online and active on this particular topic
    1:19:33
    and the what we can do with that is like if if a user logs in with their cell
    1:19:38
    phone and on the web you can we can know that they're active on their phone but maybe
    1:19:43
    inactive on the web um and then we can actually if for some reason like their account get cancelled or something like that we
    1:19:48
    can kick them out of all those sessions um which is pretty cool we can also the
    1:19:54
    way we're going to use it today is we're going to have a user list of see who's ever who who all is online at
    1:19:59
    the moment so we can see who we might be chatting with over on the right hand side there all
    1:20:06
    right so um excuse me we do need to do a few different
    1:20:11
    things to um to set this up let me just uh
    1:20:18
    look at something real quick the easiest thing to do is um phoenix provides a
    1:20:25
    generator for presence so let's just use that so mix i think it's phynxgen presents
    1:20:32
    let's see if that's it yeah there it is okay so it generated this file for us um in channels presence.ex and then it
    1:20:38
    says add your new module to your supervision tree in libchat application that's what i love about elixir it's like you could be
    1:20:46
    you could know like nothing about what's going on and it'll usually give you pretty good indication about what you need to do
    1:20:52
    next so here's our children in our application this basically starts all our supervision tree which means that
    1:20:58
    anything in here is supervised which means if it goes down for one reason or another then phoenix will try
    1:21:03
    to start it back up or application will try to start it back up in the last known good state which is pretty sweet so we can say it
    1:21:09
    was chatweb dot presence easy enough so we need to add
    1:21:14
    that to a supervision tree as well so that it'll start it up on startup of
    1:21:19
    our application and also track it and supervise it make sure it's alive and healthy as it goes
    1:21:25
    all right so let's restart our server and our presence will be started
    1:21:30
    automatically for us but let's look in that presence file it generated for us just to see what's in there it's super small i mean this is all it is for now it uses
    1:21:38
    phoenix presence and it has our otp app that's uh the app of our our phoenix
    1:21:44
    application's name is chat and then the pub sub server that we're using is uh chat up hub sub and again this is something that was
    1:21:50
    generated automatically for us when we started up phoenix with the the phoenix generator
    1:21:58
    all right now that we have it let's use it um to use it whoa i'm going to close a window not
    1:22:04
    start one we need to do something to mount here
    1:22:09
    and uh let's expand this if connected so instead of just one thing we're gonna do a couple different things
    1:22:15
    um first of all we're going to subscribe to the topic but we're also going to uh announce our presence that's a good
    1:22:21
    way to say it we're just going to tell presents we want to start tracking it and we're going to say you know chatweb.presence
    1:22:29
    and they have it has a track function and let's look at the documentation the
    1:22:34
    track function here uh it says track an arbitrary process as
    1:22:40
    a presence same with track three except track any process by topic and key so if we look at track three um up here
    1:22:48
    track a channel's process as a presence track presences are grouped by key cast as a string for example to group
    1:22:54
    each user's channels together use user ids as keys each presence can be associated with a map of metadata to
    1:23:00
    store small ephemeral state such as the user's online status to store detailed information see fetch
    1:23:06
    we don't need detailed information at the moment um but what we do want to do is uh group the user's channels by their
    1:23:13
    username in this case the usernames are random so um it shouldn't matter too
    1:23:19
    much that uh well it there could be collisions but in our
    1:23:25
    case we don't really care about the collisions um that much because it's probably it's improbable there'll
    1:23:33
    be collisions within the same room especially since the rooms themselves are random um it could happen
    1:23:38
    this is just a toy application anyway but if you're if you decide to make the next slack uh then you might want to handle um
    1:23:45
    these potential collisions and have logins and usernames if we did have like logins and usernames or set
    1:23:51
    user names um then that wouldn't be an issue uh at all but for now we're going to say for for this
    1:23:57
    process that's what self means and for the topic of the room and the room id
    1:24:03
    we're going to track the key of user name and then this map is the extra metadata we want
    1:24:09
    to store about about this particular user in this case we don't have anything in there
    1:24:15
    let me save that so now every time or when the um the page loads
    1:24:20
    here all right that is reloading a lot because we're getting error messages
    1:24:27
    that's what i was going to say next but it beat me to it um we need to handle this so all right let
    1:24:33
    me let me stop the server just so you can see this um in room live here what is what is this air image is getting why are we getting
    1:24:39
    this error message um because you can see that we're getting another message being sent to our uh our page live or sorry room live
    1:24:47
    and that message is this event of presence diff now what is presence diff if you look back in the documentation at
    1:24:53
    the very top here um let's go down here so here's how he presents track here's like
    1:24:59
    um what happens it says finally a diff of presence join and leave events will be sent to the client as they happen in
    1:25:05
    real time with the presence diff event the disc structure will be a map of joins and
    1:25:11
    leaves of the form got a map joins is the key and then each one of these is the key of the uh the thing being
    1:25:18
    tracked in this case it's our username and these are the metas we can again we can store meta information here we
    1:25:24
    haven't uh in this case but it all it includes this phoenix ref for us automatically but we don't store anything on any other
    1:25:30
    information but we what we want to do is know or handle this presence diff
    1:25:36
    because it's sent to us as we join the channel um since we joined it
    1:25:41
    it seems weird that we get the message as well but if you think about it it's not odd it's not that odd because everything is
    1:25:48
    as a message we're trying to make everything a message to and from the client and the server
    1:25:53
    so in this case the client um joins or mounts the the socket the the page and
    1:26:00
    um in mount here uh we're doing all this amount um we are starting to track the presence
    1:26:06
    and once again once the presence receives that track message
    1:26:12
    then um it sends out a diff message to all everyone that's subscribed to this particular topic
    1:26:17
    or this particular um well yeah topic and that includes the client that's
    1:26:23
    currently connected so we need to handle that uh so let's go down here and add another
    1:26:28
    um handle of info so it's another implementation handle info uh in this case it's events and the
    1:26:35
    event name is uh presence diff
    1:26:42
    and let me just verify that it's presents diff and not diff presence it is present stiff okay and the payload has joins
    1:26:49
    let's just call that joins and it also has leaves and let's uh bind that to leaves um
    1:26:55
    and that's all i care about in the event and of course it sends the socket along with it as well now for now let's just do a no reply so
    1:27:01
    we don't just get the the crazy reloads all the time because the crash and reload save that let me reshape the server
    1:27:08
    and now we should be able to load the page without it
    1:27:14
    completely crashing on us
    1:27:22
    it is taking a little while to actually finish that load and i'm not exactly sure why i may have more uh old
    1:27:27
    information in the session um
    1:27:36
    okay well we'll go with that for now but we do need to handle this presence diff um so how we're going to handle this
    1:27:41
    present stuff so let's um what do we want to do when a user leaves or joins the first
    1:27:47
    thing we want to do is we'd like to send a specific type of message to the chat client so that we can say
    1:27:54
    you know x user joined or x user left so let's do that
    1:28:02
    first um all right so we have joins we have leaves let's do
    1:28:09
    a logger info of joins just see what's in there and then leaves see what's in there as well
    1:28:17
    save that and um it's going to reload so we can see here
    1:28:23
    we have some join so we have topic split was the username that joined and then we seen this met as we do have the phoenix
    1:28:30
    ref which again we're not using but we didn't we also didn't provide any other metas and we also have chef define which
    1:28:37
    joined and uh it's in it loaded twice because of um i think because it's reloaded and then
    1:28:43
    automatically mounted from the auto reload all right so what are we gonna do for both of those
    1:28:49
    well first we want to um create a message for each of those
    1:28:57
    so let's do this let's say
    1:29:05
    we have joins we have leaves those are two separate um
    1:29:12
    excuse me two separate maps um and each of those maps has
    1:29:19
    the username i would like to reduce all those down to just a a list of
    1:29:25
    messages that we can then send to the clients so what would be the best way to do that
    1:29:32
    um well let's kind of do it um a quick and
    1:29:39
    dirty way first and then if we want to we can come back and refactor it but let's just see if we can make it work so messages is going to equal and we're
    1:29:45
    going to take joins first and for each of the joins i'm sorry the joins is a map so we need to do
    1:29:51
    map.keys send that into map keys we get all the keys of the map which are the user names
    1:29:57
    and then that way we can map those and say uh it's going to take a function and the function is going to receive the
    1:30:03
    username and then we can create a message um which the message has a uuid
    1:30:09
    you got eu id4 and the content um let's say it's going
    1:30:16
    to be username joined
    1:30:22
    like that um i think that's all we need for now
    1:30:31
    yeah the username there isn't a username um so that's going to crash when we first
    1:30:36
    do it but we'll take care of that here in a minute because well we could have the usb
    1:30:42
    system let's let's make it system for now just so it won't crash username is system
    1:30:48
    okay so those are our messages with joins and then we can also
    1:30:53
    we can say we call this join messages and then we can also create a leave
    1:31:00
    messages messages equals and then really the same thing so leaves pipe that into map.keys because
    1:31:08
    that gives us the user names and then we can email map function that's the username
    1:31:14
    and then it's going to have a uid the id 4.
    1:31:19
    the content is going to be username
    1:31:24
    uh left and then username is going to be system okay
    1:31:32
    let me end that um whoops i forgot to close out the map not
    1:31:40
    that one over here okay so now in our socket
    1:31:48
    we want to assign to the socket messages and now our messages are going to be those joins join messages
    1:31:57
    plus the leave messages and uh let's see what that gives us
    1:32:04
    all right go back to our web page we do have um the system messages coming so we'd say
    1:32:09
    that salon service joined and then genetic finish joined so uh looks like we're getting those correctly let's open
    1:32:15
    up a new one uh localhost 4000 phoenix in action here's the chat room uh and then screen
    1:32:24
    drama yeah so we have screen drama joins uh so now we have presence tracking at least so if let's like screen drama
    1:32:30
    leave yeah so screenshot on the left you see how quick that was by the way it's one of the cool things about
    1:32:35
    presents is it's super fast and performant so everyone knows now that screen drama
    1:32:41
    you know popped in take a look around i was like this is a dumpster fire and left
    1:32:48
    he is no longer with us all right what do we want to do now let's um let's build out this users
    1:32:54
    online um before we do that let me go back to
    1:32:59
    the css and for the chat messages
    1:33:04
    let's say chat messages uh any paragraphs and chat messages let's
    1:33:10
    set those margins to zero and the padding to zero just make things a little squishier
    1:33:16
    there we go that looks a little better for me to my eye and we also want to take out
    1:33:22
    remember we had this initial messages array of uh one of those messages let's take that out completely and just
    1:33:29
    have let presence track the joins and the uh the leaves
    1:33:35
    that's looking good okay next thing is these uh the user tracking
    1:33:41
    now um we know when a user joins and we know when a user leaves because
    1:33:46
    we have this handle info presence diff [Music] and um you know what let's do something
    1:33:55
    a little bit different here um let's have a type a message type uh in this
    1:34:02
    case we're gonna have this is gonna be a system message type so it's gonna come from the this the system and it's not gonna have
    1:34:08
    a username um and then down here this also is not gonna have a username
    1:34:13
    but it is going to have a type
    1:34:19
    it's a system type okay and i'm doing this because i kind of want to use
    1:34:25
    an interesting i'll show you some an interesting thing about the ability to pattern match and you'll
    1:34:32
    notice that it's just reloading itself because it's crashing because there is no username um and it thinks that there
    1:34:37
    should be a username um so we need to take care of that it's just going to keep crashing itself and reloading itself until we fix that so
    1:34:45
    let's be nice to it and fix it back to our html
    1:34:50
    we are trying to take out the message username which in this case is nothing but instead of
    1:34:56
    instead of this p tag here what if we [Music]
    1:35:01
    created a function called uh i don't know display message
    1:35:10
    display message and it's going to do that for the message um let's delete the rest of that and
    1:35:15
    that's gonna be the whole thing so now it's gonna crash for a whole different reason because we haven't defined display message um and since we're in the process since
    1:35:23
    again remember each uh page that's loaded and running is a process within um
    1:35:30
    within phoenix so the the message is gonna be called to the process itself uh or on the process itself so we need
    1:35:36
    to find display message in here now here's where the pattern matching is gonna come in inside the message there's gonna be two different types of structs
    1:35:43
    they're not really struck two different types of maps one is going to have the type of system and the other is not so we can
    1:35:52
    pattern match here so type system so whenever there is a a message that comes through as a
    1:35:58
    parameter with a parameter with and inside that map has the type of system then this is the the function
    1:36:04
    definition that's going to going to uh to match um in this case we also
    1:36:10
    want the uuid so we can um grab that and we also want the content so let's grab that as well
    1:36:16
    we can just bind all that right in the function declaration and then here's um the
    1:36:25
    content we pulled out let's just say like that i need to put out
    1:36:36
    to put a new line there okay save that um this is only going to match
    1:36:43
    for the first one but then we could say for any other display message that has no type
    1:36:48
    um we can say we all we need is the uuid and the contents and this actually have
    1:36:54
    this backwards and the um username user name
    1:37:02
    do this is actually what's gonna be displayed for messages from users and we need to do
    1:37:08
    something else for messages with um without users for now i'm going to
    1:37:14
    display nothing just to see just to make sure that our um our other display is working correctly
    1:37:19
    so this should um display a message and it does not so
    1:37:25
    let's make sure that this is being done correctly i think is it e
    1:37:32
    uh no unfind function message so there's something oh right
    1:37:39
    um it's not message.ud and it's not message.username and it's not message.content
    1:37:47
    it's just i already pattern matched those out hello okay cool so that is working again
    1:37:55
    so now we need to handle those system messages which is up here for those let's make it look pretty
    1:38:01
    similar to this um but instead of
    1:38:06
    a strong let's put like an m and we don't use your name
    1:38:12
    let's just say that uh the content there is gonna be like that and then close out the m so that should be
    1:38:18
    like um italics let's see what that does yeah so ali
    1:38:24
    broken alibi broken join and circus segment joined and then our normal messages should look normal yeah cool okay
    1:38:32
    and then anytime we get any other message type that doesn't match one of these two it'll it'll blow up on us which we kind
    1:38:37
    of want it to do we want to be loud so we know how to handle it in the future um which is good so now we need to go to
    1:38:42
    that user list so we know how to handle the joins and the leaves which is up here and if you look back in the
    1:38:50
    documentation it actually has this get by key the presence module has this git by key
    1:38:56
    function this function returns the map of presence metadata for a socket
    1:39:02
    topic key pair in this case um well you can see the example here get by
    1:39:08
    key room one and user one so we in the assigns we know we stored the the topic and we
    1:39:14
    stored the the username which are the two things we need because we also told presence to track it by the topic
    1:39:22
    and by username as the key so we can use this git by key and see all the current information
    1:39:28
    about the users um as as well as they are so
    1:39:33
    let's um let's use that in this handle info present stuff because the the time we need to
    1:39:38
    update the user list is the time when the presence diff comes through right because anytime a user leaves or
    1:39:45
    joins this presence diff message will be sent and that's when we need to update our list
    1:39:51
    so let's just say let's just bind this to user list equals chatweb presence
    1:39:58
    and then get by key was the function name and again we do have the socket which
    1:40:05
    also has the assigns so we have the topic in there and also in there we all have the
    1:40:11
    username of the current user who owns the socket
    1:40:16
    all right so for now i'm just going to log out that user list to show you what
    1:40:22
    it looks like user list user list and you'll see there's some information in there we
    1:40:28
    don't need in fact there's some information in there
    1:40:34
    that um well let's say it like this in metas you can
    1:40:40
    see that it's a list because this is where you can store information about each connection for that particular key so let's say we
    1:40:46
    did have a username list that you could you could always log in as geo
    1:40:52
    then when we looked up geo if i was on my phone and in two different browser windows then
    1:40:57
    geo would have one key but multiple of these maps
    1:41:02
    inside of this list because each one of those tracks each connection separately which is nice
    1:41:09
    however the fact that um
    1:41:16
    well you know what this this isn't the function we need now i'm thinking about it because this is getting a specific user
    1:41:22
    we don't need to get to a specific user we could do something like um you know how slack has like a geo is
    1:41:30
    writing type thing like we could we could track that information in those metas if we wanted to uh we're not gonna do that in the stream
    1:41:36
    we're already like an hour and 45 minutes into the stream so i'm not going to do that today but we
    1:41:41
    could instead let's do this list this is the one we wanted list this returns president's presences for a
    1:41:47
    socket topic and it includes all the keys and in those the metas
    1:41:52
    um so not get by key geo let's just do list and the list
    1:41:58
    takes in a uh the socket or the topic um in this case we need to put in the topic so
    1:42:05
    socket dot assigns top topic all right so that should be our user
    1:42:10
    list now let's go and look at that yeah so we have dollar ritual and then since the other page reloaded
    1:42:17
    as well we also have riviera shrink and really the keys each of those keys represents a user
    1:42:22
    so we can say we can just pull out the keys and have that be our user list
    1:42:29
    so let's just pipe that directly into map.keys and that's our user list
    1:42:36
    and so we'll also assign that so we have our messages being assigned let's also assign a user list and that will be user list and if we
    1:42:44
    save this that will now be in the signs once someone joins and or and or leaves however we're not
    1:42:50
    displaying that over here when we need to display it so we can say for user in the user list
    1:42:59
    too and again let's just put it in the p tag and say user
    1:43:06
    and the user is going to be a string because it's that key and so we don't need anything special to it
    1:43:14
    bad formatting okay save that now it'll crash on us the first time because we haven't set it up on mount
    1:43:20
    to track that user list so let's go back up here and say um user list is not going to be
    1:43:26
    in here user list is going to start out as an empty array sorry empty list i've been working in
    1:43:34
    javascript too much today all right now we have our online users um let me go back in that css before we
    1:43:41
    look at it too much uh because i also want to do this to the
    1:43:46
    user list user list div yeah
    1:43:52
    cool all right so now we can join more users um let's say localhost 4000
    1:44:00
    phoenix and action just copy this so we can put it in so now we have three
    1:44:06
    users let's add another now we should have four users yeah so everyone's getting updates
    1:44:12
    um and leaves and joins hi everybody um so quiet oberon is the first one to
    1:44:19
    speak up uh and then over here pancake mirage you know says hi back
    1:44:24
    hi back um and every every one of the browser windows gets it as soon as it happens um which is pretty
    1:44:30
    pretty cool uh so then you know quiet oberon leaves so everyone gets the message that he
    1:44:35
    left and our user's online list automatically updates to show that he's gone and then we can you know leave uh
    1:44:42
    pancake mirage can we have as well so we just left a screen melody and enigma guest just us to again
    1:44:50
    and then the screen melody says yeah but i like you all right that
    1:44:58
    in an hour and 45 minutes is building a real-time chat application with phoenix uh live view and um
    1:45:06
    again i am i am looking at the chat if you have any questions or comments please uh put it in there because i am going to wrap it up here um
    1:45:13
    thank you for joining me this was uh it's always interesting to do stuff live um because you always encounter error
    1:45:21
    messages that you haven't before it's always it's always a treat to see
    1:45:26
    what comes up but again if you go to phoenixinaction.com phoenix gosh i can't spell today
    1:45:32
    phoenixinaction.com it'll take you directly to manning's site for the phoenix in action book that's
    1:45:37
    the book i wrote about phoenix this book came out a couple years ago
    1:45:42
    and it does not cover live view however there are some huge things you need to
    1:45:48
    know before you get into live view that this book does cover live view itself came out about
    1:45:54
    two months after this book was published and it could take up its own book and i have been thinking about maybe
    1:45:59
    doing like some sort of supplements or appendix or something like that that um that covers live view a little bit but live view is its own topic
    1:46:06
    however if you're new to elixir or new to phoenix then this book should get you up to speed um
    1:46:12
    to to where you can jump into live view very easily and
    1:46:18
    [Music] yeah i hope you buy it and also if you don't know any elixir at all
    1:46:24
    it's it provides a pretty i think a pretty thorough overview of the elixir programming
    1:46:29
    language enough to get going i do see some uh some questions here in the chat the first is um is phoenix something you would use by
    1:46:36
    itself or is it primarily for the real-time socket parts now it's definitely something that you can use by
    1:46:41
    itself i do know that there are plenty of websites that um that are served by phoenix that um
    1:46:47
    aren't really using the live view stuff at all i'll show you one thing that i created
    1:46:54
    it actually does use uh sockets um but if you're struggling with regex
    1:46:59
    and how regular expressions work in phoenix then this is something you can use this was actually created for a competition when live view was first
    1:47:06
    announced um to basically explore live view and how you can use it but
    1:47:11
    like first you hear you know you can put in your input here so is phoenix something
    1:47:17
    you would use by itself let's just say like that and then you can start putting your pattern here so let's say you wanted to
    1:47:24
    match out phoenix and itself uh let's see if we can do that so you know as you type not only does um
    1:47:31
    there was the function call that you need in order to you know copy and paste this this world
    1:47:37
    of the regex into your own application code but it also has like the results and the matches
    1:47:42
    um which i think is pretty cool so in between phoenix and then itself so it doesn't match that
    1:47:49
    but then we can like you know pull those parts out so it has real-time error handling as well
    1:47:54
    so our first match is phoenix and then the next thing we wanted to match was itself um
    1:48:01
    yeah so we see the match one is phoenix match two is itself um so there's things you can do in live
    1:48:06
    view that um are really cool and you also see that you know the the url itself is being updated in real
    1:48:13
    time which is is pretty cool i think so i can like copy and paste this and um like you can go there
    1:48:19
    you can see that exact same url or exact same um the thing from uh just copy and pasting
    1:48:25
    it to someone saying hey i found this regex to work for your situation um try that out um anyway
    1:48:32
    uh how that that's an answer to the question of do you have to use live view or the the real-time capabilities um you
    1:48:39
    don't and i will say like let me show you um phoenix let's just load the page and uh
    1:48:46
    the page loads um when i first loaded the page here it sent 200 so it sent a good response in four
    1:48:54
    milliseconds i mean it connected to the socket in 55 was a microseconds um
    1:49:00
    phoenix is since it's compiled uh it is insanely fast so um one of the things
    1:49:07
    that phoenix brags about is that it can handle so many uh simultaneous connections at one time so if we go to
    1:49:13
    like i think it's in channels it talks about the capabilities uh
    1:49:18
    phoenix channel things you know um now let's try in the guide for channels
    1:49:27
    yeah so this just talks about how um channels works and some some information about it but then this
    1:49:32
    uh this i love this paragraph this architecture scales well phoenix channels can support millions of
    1:49:38
    subscribers with reasonable latency on a single box passing hundreds of thousands of messages per second
    1:49:43
    and that capacity can multiply by adding more nodes to the cluster one thing that i didn't even go over in
    1:49:50
    in this particular thing uh in our chat application is that it has the ability to um
    1:49:58
    to do navigation live as well so there's some uh some functions that you can use to handle navigation through the sockets
    1:50:05
    which means that um when you navigate from one page to the other if you think about normal servers um they basically have
    1:50:12
    amnesia like they forget everything about you the moment you click the next link that means you've got to send them your
    1:50:18
    session information and they've got to re-um revalidate that you are able to
    1:50:23
    see the page check your permissions and then re-render like every piece of html that's on your page including this phoenix in
    1:50:30
    action chat header that never changes or uh the whole javascript bundle that
    1:50:36
    um that hasn't changed either and so hopefully there's things that that they do to to cache that information but
    1:50:42
    still that's a lot of information to send on everything but if you you know go through live navigation all that um
    1:50:48
    is is updated um with very small changes um which is pretty cool
    1:50:54
    another thing a little side project that i've done um that um right now has a couple errors show up
    1:51:00
    but i'm gonna show you anyway uh is um
    1:51:06
    oh dang i forgot the name of it that tells you how long it's been since i've looked at it
    1:51:12
    um is it flight oh yeah flightcharts.io um so i'm i'm a pilot and but i also do
    1:51:18
    a lot of sim flying and i wanted an easy way to search for airports and find flight charts for it from the faa and
    1:51:24
    you can see that the database for the faa database hasn't been updated since uh december so the charts
    1:51:29
    themselves won't work but you could still search for airports and you know identifications names and cities but watch how fast this
    1:51:36
    automatic search automatic completion happens so let's just say i search for uh san diego
    1:51:41
    so if i search sand like all these things come up this is live view populating this page in real time
    1:51:47
    through the search um and then like as i continue to drill down you can see that the the page updates so fast
    1:51:54
    and this is i okay i'll here's this and um elixir regex and probably
    1:52:02
    four other side projects are all hosted on the smallest um digital ocean
    1:52:09
    droplet that you can get each in their own docker container and while they aren't um
    1:52:16
    you know they're not huge um they don't get a whole lot of traffic
    1:52:22
    they still are are so fast um that it is very impressive to me anyway i love phoenix
    1:52:27
    and what i can provide um let me show you my website this is not
    1:52:32
    hosted with phoenix but this is just straight html but you can see that it's been a little while since i've posted something the book took a lot of
    1:52:38
    my writing energy but hopefully in there you can find some things that are very interesting a lot
    1:52:44
    of things are still applicable um especially in terms of ecto and where you can connect to databases which i didn't cover at all
    1:52:50
    today and then also if you go to my youtube channel i have a playlist in here um let me uh
    1:52:58
    let's see wow playlist let's say as i'm logged in as me you can
    1:53:03
    see all my my personal playlist but that's okay um i have one called
    1:53:11
    uh where is it talks i've given there it is so if you look at talks of given um and
    1:53:17
    this is linked to from a website maybe that's how i should have gotten there so if you go to geoffreylesson.com uh then talks um here's some
    1:53:26
    um some of the talks i've given over the years that you can take a look at um but in this uh this you know there's
    1:53:33
    some phoenix information in here that's pretty fun um this one is uh phoenix updates through the browser
    1:53:39
    i did that it's like a 20 minute talk did that a meet-up and then i did a longer version of that
    1:53:44
    just a couple weeks ago for a go-to conf and hopefully those will be online soon but yeah go take a look at those if you
    1:53:51
    want more information about phoenix and elixir and some of the fun things you can do i like them to dabble with stuff so like
    1:53:56
    i do stuff like midi devices and external steering wheel displays and crazy things like that with elixir which is really fun
    1:54:02
    um so yeah thanks cs255 i appreciate that for the for the question
    1:54:08
    and for the response um any other questions from anyone um happy to answer them
    1:54:15
    otherwise we're gonna start wrapping this thing up um i don't know if it's dinner time for any of you but it is dinner time for me
    1:54:22
    and uh i'm getting a little hungry so let me put this uh screen back up here um again twitles40
    1:54:29
    i believe that's like a combination of twitter and lessel um i didn't come up with the with the
    1:54:35
    code manning did great code uh but twit list is kind of funny so twit list40 gets you 40
    1:54:40
    off at manning anything in manning go go check it out i'm at twitter at geolessel.com um
    1:54:47
    not george geolessel so um like chris mccord who created
    1:54:53
    elixir has made some cool stuff including like a um a twitter clone uh not a clone that's kind of like a
    1:55:00
    clone in live view that is really neat um so yeah go check out my twitter go check out my github i've got a lot of
    1:55:06
    things like my dot files on github as well so if you want to check those out all right so again you know my um my
    1:55:12
    twitter account so message me there if you want to contact me directly and uh message me on youtube if you if
    1:55:19
    you see one of those videos and you want to get in touch with me let me know i really appreciate you showing up i do uh great way to spend a friday afternoon
    1:55:25
    slash evening and i'm glad you're here with me uh again i'm jeffrey lessel and um thank you so much for joining