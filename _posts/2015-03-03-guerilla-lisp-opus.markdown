---
layout: post
title: Guerilla Lisp Opus
categories: [common-lisp]
visible: t
---

> Path: archiver1.google.com!news1.google.com!newsfeed.stanford.edu!news.ems.psu.edu!news.litech.org!news-xfer.cox.net!prodigy.com!newsmst01.news.prodigy.com!prodigy.com!postmaster.news.prodigy.com!newssvr14.news.prodigy.com.POSTED!df898341!not-for-mail
> From: "Will Hartung" <wi...@msoft.com>
> Newsgroups: comp.lang.lisp
> References: <c29fzumv8r9.fsf@no-knife.mit.edu> <u7lm4d3vl7.fsf@snapdragon.csl.sri.com> <_hMy9.1126$Aq5.112540@newsread2.prod.itd.earthlink.net> <4wunnhj3b.fsf@beta.franz.com> <FW8z9.2861$Aq5.303614@newsread2.prod.itd.earthlink.net> <4wunmbjul.fsf@beta.franz.com> <H_uz9.4624$Aq5.499904@newsread2.prod.itd.earthlink.net> <LFIz9.1032$Ya2.36121645@newssvr14.news.prodigy.com> <MPG.18392bb6dfdeaff9896d6@shawnews.vc.shawcable.net> <8kRz9.4286$y56.188794115@newssvr13.news.prodigy.com> <aqphij$du8$1@otis.netspace.net.au>
> Subject: Guerilla Lisp -- The OPUS (was Re: some stuff about the 2002 International Lisp Conference in SF)
> Lines: 347
> X-Priority: 3
> X-MSMail-Priority: Normal
> X-Newsreader: Microsoft Outlook Express 6.00.2600.0000
> X-MIMEOLE: Produced By Microsoft MimeOLE V6.00.2600.0000
> Message-ID: <4caA9.1572$_27.85095759@newssvr14.news.prodigy.com>
> NNTP-Posting-Host: 63.202.104.87
> X-Complaints-To: ab...@prodigy.net
> X-Trace: newssvr14.news.prodigy.com 1037119360 ST000 63.202.104.87 (Tue, 12 Nov 2002 11:42:40 EST)
> NNTP-Posting-Date: Tue, 12 Nov 2002 11:42:40 EST
> Organization: Prodigy Internet http://www.prodigy.com
> X-UserInfo1: FKPO@SNGPBWWSQDYEZOD]_\@VR]^@B@MCPWZKB]MPXHZUYICD^RAQBKZQTZTX\_I[^G_KGFNON[ZOE_AZNVO^\XGGNTCIRPIJH[@RQKBXLRZ@CD^HKANYVW@RLGEZEJN@\_WZJBNZYYKVIOR]T]MNMG_Z[YVWSCH_Q[GPC_A@CARQVXDSDA^M]@DRVUM@RBM
> Date: Tue, 12 Nov 2002 16:42:40 GMT
> Xref: archiver1.google.com comp.lang.lisp:46391
> 
> "Coby Beck" <cb...@mercury.bc.ca> wrote in message
> news:aqphij$du8$1@otis.netspace.net.au...
> > You used lisp to do it?  It's relevant!  Send that opus over... :)
> 
> I got several requests for this thing, so I figured I'd post it rather than
> send out several copies.
> 
> ----- Original Message -----
> From: "Brian Palmer" <brian@invalid.dom>
> Newsgroups: comp.lang.lisp
> Sent: Monday, November 11, 2002 2:52 AM
> Subject: Re: some stuff about the 2002 International Lisp Conference in SF
> 
> 
> > Will Hartung wrote:
> > >
> > > Lisp is a tool as much as Javascript is a tool. I used it in a Microsoft
> > > shop writing J2EE Java code for Suns to create Java code.   ...
> > > And ya know what? The client had NO IDEA how I was doing "my
> > > magic". Lisp was my tool, yet Java was their solution.
> >
> > I'd love to hear more about how this is done, either your case in
> > particular or a pointer to some articles/books which describe something
> > like this.  I'm intrigued!
> 
> Our application is a J2EE "Care Management System". The basic premise is
> that an organization such as a Medical Group would enroll patients into
> particular programs to help track their status. Example programs are Cardio
> Vascular Disease and Diabetes. I think I'm not alone here on working on such
> a project.
> 
> The Care Manager would engage the patient with pre-planned questionnaires
> that ask about the patients current conditions, habits, history, etc.
> 
> Then, while the patient is within the program either the patient would log
> in directly, or the Care Manager would contact them with followup questions
> and status. So, over time, the data entered into the system would help with
> things like tracking a persons weight, or blood pressure or even medication
> interactions.
> 
> The key to the system was a set of "Rule logic" that checks the data and
> creates the next step in the workflow for the patient. For example, the
> system could see that a patients weight is going up over a short period, and
> that may be a trigger to alert their physician. Things like that.
> 
> All of those rules are considered "clinical content", and they're written
> by, of all things, Clinicians. Clinician are the medical knowledge for the
> project, but they are NOT "computer people".
> 
> I had written a scripting language which made it easier to create these
> rules, because it made access to the data model much easier and abstracted
> the higher end results of the rules (tasks, messages, etc). All of the
> clinical content is supposed to be written in this scripting language called
> RSL. It's your basic ALGOLesqe scripting language, with simple IF-THEN
> statements. Ideally, all of this would be done as some kind of simple expert
> system, but what was originally specified and what we have today are
> different beasts, so we work with the tools we have.
> 
> RSL is organized into execution blocks called Packages, and these were
> associated to the questionnaires. While there are, essentially, subroutines
> and functions in RSL, the real level of abstraction was the Package, with a
> list of variables needed from the database enumerated at the top the file,
> in a pacakge-wide namespace, and then followed by the logic.
> 
> The clinical content was defined by the clinicians in spreadsheets. They
> would specify the variable they were populating, and how it was calculated.
> Later they would specify messages based on variable results.
> 
> A very simple example:
> HEIGHT_FEET -- Height in Feet (prompted variable)
> HEIGHT_INCHES -- Height in Inches (prompted variable) [ For "What's your
> height in feet and inches"]
> WEIGHT_LBS -- Weight in pounds (prompted variable)
> TOTAL_HEIGHT = HEIGHT_FEET * 12 + HEIGHT_INCHES
> WEIGHT_KILOS = WEIGHT_LBS / 0.6
> BMI = WEIGHT_KILOS / TOTAL_HEIGHT
> 
> BMI is the "Body Mass Index", and this isn't the actual calculation, just an
> example. But basically the BMI lets us easily determine if someone is too
> heavy or or not for their size. So, if you were 4ft 2in and weighed 300lbs,
> you're "too heavy".
> 
> So, given these variables, they would create a rule. (These ratings are
> complete BS, I just made them up.)
> 
> BMI > 4 -- Message "You're too heavy"
> BMI > 3 -- Message "You're just right"
> OTHERWISE -- Message "You're too light"
> 
> Now, when given this rule, the BMI variable would actually be defined in a
> completely different spreadsheet. If I were to code this in RSL, I'd write
> something like this:
> 
> PACKAGE TEST
> VAR HEIGHT_FEET = HEIGHT_FEET // This is how we access vars in the DB
> VAR HEIGHT_INCHES = HEIGHT_INCHES // The name after the = identifies the
> variable
> VAR WEIGHT_LBS = WEIGHT_LBS
> WORKVAR TOTAL_HEIGHT = NUMBER // Workvars are local variable, and note that
> they're typed.
> WORKVAR WEIGHT_KILOS = NUMBER
> WORKVAR BMI = NUMBER
> 
> TOTAL_HEIGHT = HEIGHT_FEET * 12 + HEIGHT_INCHES
> WEIGHT_KILOS = WEIGHT_LBS / 0.6
> BMI = WEIGHT_KILOS / TOTAL_HEIGHT
> 
> IF BMI > 4 THEN
>     MESSAGE "You're too heavy"
> ELSEIF BMI > 3 THEN
>     MESSAGE "You're just right"
> ELSE
>     MESSAGE "You're too light"
> ENDIF
> 
> Pretty straight forward.
> 
> But as an RSL Coder, I had to look up BMI, find out that it used
> TOTAL_HEIGHT and WEIGHT_KILOS. Then I had to look THOSE up, and find out how
> they were defined. Finally, I had to ensure that they were in the proper
> order, etc.
> 
> The issue was, of course, that there were hundreds of rules and variables,
> not simply these few. The other issue was that these were being developed
> while they were being coded, and the changes were all very local.
> 
> If they changed the definition of BMI, I'd have to go through the code, find
> BMI, find out what variables it was using, and if I was thorough, I'd check
> to see if the old variables weren't being referenced any more and delete
> them. The key being that all of these rules and variables were very
> interdependent, so any changes had the potential to ripple through all of
> the code. Plus, they were not quite sure which rules (like the BMI rule)
> were to fire for which questionnaires. So, if they decided that
> Questionnaire A no longer needed the BMI rule, they would take it out. But
> since the code was basically designed to handle the individual
> questionnaires, then I'd have to change that code as well. Or worse, if BMI
> was used in several questionnaires, I'd have to change all of the files that
> they were referenced in, and ensure that they're all using the new logic. It
> was a real pain.
> 
> Now, I saw this issue immediately, and I thought it was terrible.
> 
> While I had written the RSL compiler, which converts the RSL into Java, (I
> didn't design the language), I had never actually USED RSL for clinical
> content. I had never seen the actual clinical content the "Scripters" were
> supposed to be creating RSL from. The original goal was that RSL would be
> easy enough for the Clinicians to do it themselves. That, obviously, did not
> happen.
> 
> So, this was my first exposure to real, authentic Clinical Content, and
> these relationships between the variables, and their rules was glaring.
> 
> So, what I did was I started to code up the spreadsheets I had as simple
> structures.
> 
> (DEFVAR WEIGHT_LBS type NUMBER desc "Weight in Lbs" class DBVAR)
> (DEFVAR WEIGHT_KILOS type  NUMBER desc "Weight in kilos" class WORK INIT
>     (set WEIGHT_KILOS (/ WEIGHT_LBS 0.6)))
> (DEFVAR BMI type NUMBER desc "BMI" class WORK INIT
>     (set BMI (/ WEIGHT_KILOS TOTAL_HEIGHT)))
> 
> (MESSAGE BMI-1
>     (WHEN (> BMI 4) (MESSAGE "You're too heavy"))
>     (WHEN (> BMI 3) (MESSAGE "You're just right"))
>     (OTHERWISE (MESSAGE "You're too light")))
> 
> I simply just typed everything in like this, just filling in the stuff I
> knew into a Lispy syntax, not even sure what I was going to do with it. But
> I was confident that I could always quickly generate something if the
> project dragged because of this and drop back into "pure RSL".
> 
> After I coded the Variables and rules into these structures, I started
> writing code to manipulate them. To pick out the dependencies and keep
> track.
> 
> The beauty of this was that my Lispy stuff was almost one to one with the
> specs, save for being in prefix vs infix. It was also very clear very
> quickly that this was going to be a great time saver. The dependencies were
> "self declaring", just by using a variable in an expression. If I were to
> get a change in a calculation, I could simply go to the variable definition
> and change it, without worrying about the change bubbling through the code.
> 
> The goal started to simply capture all of the info I had available (a simple
> spreadsheet), and capture it into a form that was easily manipulated by the
> computer. When changes came, I captured those also.
> 
> Since there was so much commonality to the rules and their structure, basic
> problems with the system were solved just once.
> 
> So, in the end I simply wrote a basic "RSL Compiler" to convert these
> structures. I was able to define the relationships between the packages and
> the rules they contained, as well as the packages and questionnaires that
> fed them. And it was all done with little thought. Little up front planning.
> Like I said in the beginning I did not know what I was really going to do
> with the information when I started, but I knew that a) changes were coming,
> and that b) it was going to be a lot easier to work with the "code as data"
> concept than just straight code.
> 
> Once I had large chunks of the rules and variables coded, the solution
> started to present itself. By using the implicit declarations of the the
> variables within other variables and rules, it was simple to organize the
> data and build dependencies to generate the code correctly. In this case, I
> would simply say that a Package contained the BMI-1 message rule, and the
> compiler drags in all of its dependents, structured and ordered the
> declarations properly, and generated the correct code. If the package
> contained BMI-1 and BMI-2, then the common variables would only be used
> once, everything would be simply organized. No real rocket science here.
> 
> With the compiler doing all of the work, the client was able to send quick
> changes over through email after short dicussions via AIM. Once I got the
> change, it was usually simple to implement because the monsterous side
> effects were all handled automatically. Adding or removing a variable from a
> rule could eventually add a dozen or more dependent variables into the final
> code, but the change was simply adding the variable to the rule.
> 
> When systems have a lot of code, they tend to gain a momentum of their own
> and become resistant to change. This system had almost no momentum,
> regardless of the number of rules. This lack of momentum also made testing
> simpler because as long as the actual information from the original
> spreadsheets were captured accurately, the rest of the system would, mostly,
> just work. If it didn't work, it was a clinical issue, but not a technical
> one.
> 
> Late in the project, they completely changed some major pieces of the
> specification. Had this been done the original way, I would have had to go
> to each rule implementation, beat it into submission, make sure I didn't get
> any typos or drop a variable, etc. With the compiler, I added some macros,
> once, tweaked the compiler, once, and made some simple changes to the Lispy
> source code, and the change was done.
> 
> It was also very easy to do things like discover basic things like what
> rules depended on what variables, or what variables were simply not in the
> spec. That was all done interactively at the listener by simply querying the
> data structures that were created and writing a few simple functions.
> 
> The other fella working on his own rules had less to do and took longer and
> was much more resistant to changes than I was, and for good reason. I
> described to the client that I was collecting all of the requirements and
> specifications into a large cloud of Stuff and any time they asked, the
> cloud would rain down and create a solid structure. But, while in the cloud,
> anything can easily be changed. So, while I was keeping the specs in an
> etheral state, the other fella had to chisel his into stone by using the
> straight RSL code. The later into the project, the more solid his structure
> and more difficult any changes were.
> 
> I even had time to optimize some of the rules. There were several rules like
> IF a AND b then MESSAGE X, ELSE IF a AND c THEN MESSAGE Y. Only the rules
> had several common variables. I was able to capture those rules just as
> specified, with the redundant conditions, and had the compiler simplify the
> expression to get the common ones factored out.
> 
> Finally, I didn't "ask permission" to do this, I simply did it. I didn't go
> to my boss, or the client and say "Hey, I want to use Lisp here". The task
> was "convert this spreadsheet into RSL". THEY wanted the RSL Source Code for
> the rules, and that's what my tool created for them. About a week into the
> task, my boss wanted some status, and by that time I already had all of the
> rules keyed into my format, had the basic structure down, and was moving
> ahead. He's not a Lisp Guy, and tends to fear tools, but I assured him I was
> ahead of schedule, that changes were easy, and should I ever starting
> falling behind, I was always able to "snap shot" all of the Lispy stuff into
> pure RSL and go from there, not losing any time in the process.
> 
> I think the idea of being able to easily drop back into "conventional mode"
> was a reassurance. If all else failed, I could always go back to doing it
> the Hard Way. But, certainly there are cultural issues involved and every
> place is different.
> 
> It's biggest problem, in the end, was that it used too many parentheses in
> the generated code, and tended to run long IF statements together on a
> single line. I didn't put the time into writing a prettier code generator,
> although it was nice and indented, and looked really good. It was even
> spitting out comments for what rules were being implemented in which parts.
> 
> But, the real nice part was that later, when I wasn't doing any more work on
> it, they took all of the generated RSL and reorganized it as RSL. It
> probably took the guy more than a week to do what I would have done in 30
> minutes, but it showed that the RSL code was viable, useable and readable.
> 
> I couldn't have done this without Lisp simply because I would have had to
> work on grammars, parsers, lexers, and crap like that. I relied on the
> reader and macros to make my "language". I was never behind (save at one
> point when my generated RSL was too big for Java, it has an implicit class
> size limit), and I took every change they threw at me. I was able to do
> simple data manipulations and queries using the listener, I never had a more
> sophisticated interface than simply a text editor. No GUI, no nothing.
> 
> Overall, it was a complete Lisp hack. Relying on lots of global structures,
> I was constantly zapping all of the data, and reloading things, but it was
> never slow enough to matter. It was also totally evolutionary. No plan, just
> baby steps each way. When I found that I was way ahead I was able to put
> time into the optimizers and such, and I had the capacity to absorb the
> changes that they were throwing at me.
> 
> Obviously not every application falls into the mold. This was something that
> had a nice, regular structure, and the RSL was easy to compile code into.
> Also, being a code generator, it's not practical in environments where
> others do NOT have the tools, and who will end up working on the generated
> code rather than the abstract meta language. When they tore my generated
> code apart for a later version, there was no going back to my original meta
> code. Also, I was fortunate to be the only one on the task, meaning I didn't
> have to write the tool for others to use, which would have been a severe
> time sink.
> 
> It was also really important in that it gave ideas on how we can possibly
> redirect how the content is created in the future. If the clinicians can
> create those spreadsheet specs that they sent me, then they are really close
> to being able to create something just a little more regular and be able to
> create the clinical content directly, whether with S-Expr or with a new
> grammar and language.
> 
> The key is, though, that a lot of this went under the radar. It was a
> "results over process" success. If your group is focused more on process
> than results, then there's not much you can do. But the other thing is that
> it was nice to bring Lisp into the everyday work world for what I was doing.
> While people create little scripts all day long, they never seem to think
> that they can do the same in Lisp, and leverage them even better later on.
> 
> Also, one last thing, this was my first major attack of something in Lisp.
> The first time I really used Lisp "in anger". I didn't leverage years of
> Lisp experience to pull this off, just years of sitting around here on
> c.l.l. and occasionally dabbling a little. I relied mostly on the Hyperspec
> to figure things out.
> 
> It was great fun to do, because I had all of the rules keyed in. So,
> whenever the next stage in the compiler was finished there was lots of code
> generated. Whenever a change was made, it was nice to get the change, say,
> "Hang on", and a minute later say "All done!", with that minute consumed by
> making the change and regenerating the code. The best feature of the tool
> was the confidence it gave me that the changes were correct, knowing that
> changing A to B was all that was necessary. With large code bases, simple
> changes can be very simple, but they don't need to get too complex before
> you start doubting and questioning whether you had caught everything.
> 
> In the end, the Lisp code was about 1800 lines. The rule code was about 8000
> lines, and it generated a boat load of RSL. It was great to see how the
> changing of a single variable in one of the rules changed an RSL file from
> 1700 lines to 2500 lines, and that alone showed how important this process
> was to saving my sanity.
> 
> Regards,
> 
> Will Hartung
> (wi...@msoft.com)

