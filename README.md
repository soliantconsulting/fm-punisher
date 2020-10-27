![A screenshot of a cell phone Description automatically
generated](media/image1.png)



[Preliminary Note](#preliminary-note)

[What is it?](#what-is-it)

[How does it do it?](#how-does-it-do-it)

[What do I need?](#what-do-i-need)

[How do I use this?](#how-do-i-use-this)

[General Navigation](#general-navigation)

[Create a Config record](#create-a-config-record)

[Run a Test](#run-a-test)

[The Scripts & Comparing Results](#the-scripts-comparing-results)

[Feedback requested](#feedback-requested)

Preliminary Note
================

Punisher started out as a strictly internal Soliant tool for using
during FileMaker ETS beta testing. As such it may be rough around the
edges, especially when it comes to UI and UX. Please raise a GitHub
issue with your feature requests or with feedback for improvements.

What is it?
===========

Punisher tries to test the speed of FileMaker Server running on
different configs and it does it by spawning simultaneous (concurrent,
parallel) PSoS sessions that run through 16 expensive scripts.

Punisher basically abstracts out the effect of the client\'s processing
power or the client-to-server network speed/latency; it only tests what
the server is capable off. Punisher also abstracts out any design choice
differences between different solutions, it always runs the exact same
tests, just on different hardware configurations.

The intent is to document how different configurations and different
versions of FileMaker Server make a difference and to answer basic
questions such as:

-   Is FileMaker Server 19 faster than 18, in what areas?

-   Is FileMaker Server on Linux faster than on Windows?

-   What is the effect of faster cores? Or more cores?

How does it do it?
==================

Every test run will spawn a preset number of simultaneous PSoS sessions
and each PSoS session will run through the same set of scripts at
exactly the same time.

The scripts are meant to be a relevant cross-section of different types
of operations: purely computational efforts, record creation, record
sorting, record editing, \... As such, they tax different areas of
FileMaker Server. Some scripts are more taxing on the server-side script
engine process, some are more taxing on the database server process.

What do I need?
===============

Punisher consists of four files:

-   Punisher_YYYYMMDD: this is the main file with the scripts and the
    test results. The date stamp in the file name is the version. This
    file is likely to change often.
    
-   Punisher_test_data: this one contains a small test table and all the preferences

-   Punisher_small and Punisher_smaller are utility data files to give
    the scripts something to work with. These files are not going to
    change often if at all, so you only need to download them once. Grab
    the 7z archive from Dropbox folder, it contains these two
    files: https://www.dropbox.com/s/0ckqo1u2lojk7ov/Punisher_utility_files.7z?dl=0

![A screenshot of a cell phone Description automatically
generated](media/punisher_2020-10-27_13-46-47.png)

Download the four files, host them on your FileMaker Server and you are
all set.

Credentials for the main file: ets / ets


How do I use this?
==================

General Navigation
------------------

The Punisher icon in the top left will always take you back to the main
menu screen.

The Hamburger icon in the top right will pop open a navigation menu.

Create a Config record
----------------------

In the Config section you create a record to document your particular
FileMaker Server:

-   What operating system does it run?

-   How many cores at what speed?

-   How big is the hard drive and what type is it (spinning platters,
    SSD...)?

-   How much memory is installed?

![A screenshot of a cell phone Description automatically
generated](media/image3.png)

You can export a config record and all of its associated test results
from here too, and you can import one.

Run a Test
----------

From the Hamburger menu on the top right and select "Run a New Test"

![A screenshot of a cell phone Description automatically
generated](media/image4.png)

If you intend to run just one load-simulation test, then you can specify
the number of concurrent PSoS sessions (users if you will) to spawn.

The 'data restoration' feature is only relevant if your FileMaker Server
is 18 or 19.0.

Enter the build number of your FileMaker Server, you can find it on your
FileMaker Server admin console dashboard, the build number is the last
number in the full version number:

![A screenshot of a cell phone Description automatically
generated](media/image5.png)

The build number is used later on in comparing the results between
different builds of the same FileMaker Server (which is mostly useful
during beta testing).

You can set the start time and abort time for the test run by using the
+ buttons to add x minutes to the current time.

![A picture containing looking, sitting, standing Description
automatically generated](media/image6.png)

Choose your configuration and select the scripts you want to run.
Typically, you would select all scripts except if your FileMaker Server
is 16 or 17. The scripts use some features that are only available in 18
and up.

If you just want to run the number of simultaneous sessions that you
entered up top then click the blue button marked "Run this test":

![A picture containing drawing, bird Description automatically
generated](media/image7.png)

If you want to run a set of simulations using a single PSoS, 5, 10 and
20 simultaneous PSoSes then use the blue button marked "Run test with 1,
5, 10 and 20 sessions":

![A picture containing bird, drawing Description automatically
generated](media/image8.png)

Punisher will show a new window and will wait for the set start time.

![A screenshot of a cell phone Description automatically
generated](media/image9.png)

Through an OnTimer event it will check the progress of each PSoS session
until all the tests are performed and then show the "Done" dialog.

![A screenshot of a cell phone Description automatically
generated](media/image10.png)

The Scripts & Comparing Results
===============================

Comparing test runs by script is the most useful view into the test
results.

Navigate to the Scripts section and read up on what the script does.
Keep in mind that the scripts are meant to do something that is
measurably slow; there are ways to make things faster obviously, but the
point is to make FileMaker Server work hard.

For each script you will the individual test run results in seconds and
info on what config it was run on plus how big the overall load was at
the time.

![A screenshot of a cell phone Description automatically
generated](media/image11.png)

The same numbers are shown when you click on "Show Details" but this
time the results are shown in a JS DataTables view that is searchable
and sortable.

![A screenshot of a cell phone Description automatically
generated](media/image12.png)

Even more interesting is what you get from the "Show Comparison" view.
Here the results are shown in a Pivot Table so that you can
slice-and-dice the results exactly like you want them to. You can drag
and drop various data elements between the rows and columns and also
change the type of Table with all the provided controls.

![A screenshot of a computer Description automatically
generated](media/image13.png)

You can also filter it down by omitting various elements.

Here are those same test results but filtered to only show runs on
Windows and only on AWS machines:

![A screenshot of a computer Description automatically
generated](media/image14.png)

And here is a view that compares CentOS to Windows on AWS boxes only:

![A screenshot of a social media post Description automatically
generated](media/image15.png)

The number of comparisons you can make here are almost endless.

Feedback requested
==================

Please provide feedback through GitHub issues or find us on
community.claris.com.
