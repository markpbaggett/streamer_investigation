Proprietary Assets
==================

All proprietary assets can be found at :code:`\home\share\content`.

This content consists of 596 GB of assets and associated files.

The following sections describe the content in more detail.

Organization
------------

The files are organized by vendor only. When multiple works are provided by a vendor, they are stored in the same directory.

Relationships between related files are maintained in a few ways including via naming convention. If a file name is
shared, the two works are related. There is no real consistency in how this is done however, and this is not always the
case.

One common pattern is the same file name with different extensions.

You can see this in the following example from pbs:

.. code:: shell

    -rwxr-xrwx.  1 root   root   857281042 Dec 31  2013 NPA700D4-1.mp4
    -rwxr-xrwx.  1 root   root      125682 Jun 18  2015 NPA700D4-1.vtt
    -rwxr-xrwx.  1 root   root   957928294 Dec 31  2013 NPA700D4-2.mp4
    -rwxr-xrwx.  1 root   root      166771 Jun 18  2015 NPA700D4-2.vtt
    -rwxr-xrwx.  1 root   root   723216261 Dec 31  2013 NPA700D4-3.mp4
    -rwxr-xrwx.  1 root   root      135174 Jun 18  2015 NPA700D4-3.vtt
    -rwxr-xrwx.  1 root   root   739403142 Dec 31  2013 NPA700D4-4.mp4
    -rwxr-xrwx.  1 root   root      134459 Jun 18  2015 NPA700D4-4.vtt
    -rwxr-xrwx.  1 root   root   754450501 Dec 31  2013 NPA700D4-5.mp4
    -rwxr-xrwx.  1 root   root      126944 Jun 18  2015 NPA700D4-5.vtt
    -rwxr-xrwx.  1 root   root   824164403 Dec 31  2013 NPA700D4-6.mp4
    -rwxr-xrwx.  1 root   root      125577 Jun 18  2015 NPA700D4-6.vtt

While this pattern is common, it is not universal even within a single vendor. For example, the following files from pbs
use a different pattern:

.. code:: shell

    -rwxr-xrwx.  1 root   root  1888576602 Dec 31  2013 PAL701D4.mp4
    -rwxr-xrwx.  1 root   root       63636 Dec 31  2013 PAL701D4.txt
    -rwxr-xrwx.  1 root   root         619 Dec 31  2013 PAL701D4 with Captions.smil

A third pattern which I don't completely understand has multiple vtt files with one hidden and one not hidden. For example:

.. code:: shell

    -rwxr-xrwx   1 root   root        4096 Sep 14  2018 ._CC MAJOR.scc
    -rwxr-xrwx   1 root   root      250928 Mar 30  2017 CC MAJOR.scc
    -rwxr-xrwx   1 root   root  1554055392 Sep 13  2018 majorhd720.mp4
    -rwxr-xrwx   1 root   root        4096 Sep 14  2018 ._majorhd720.vtt
    -rwxr-xrwx   1 root   root      134016 Sep 14  2018 majorhd720.vtt

Another pattern that can be found is where the video files are in a directory and the closed captioning files are in a
sibling directory called :code:`cc`. When this happens, it's not clear how to tell which closed captioning file goes with
which video file. For example, the ambrose files look like this:

.. code:: shell

    alls_well_that_ends_well_continuous_cc.mp4
    america_the_new_found_landcc.mp4
    anthony_cleopatra_continous_cc.mp4
    antony_cleopatra_continous_cc copy 2.mp4
    as_you_like_it_continuous_cc.mp4
    bio_plant_ch1_323bc.mp4
    bio_plant_ch2_1682.mp4
    bio_plant_ch3_1694.mp4
    bio_plant_ch4_1838.mp4
    bio_plant_ch5_1866.mp4
    bio_plant_ch6_1886.mp4
    bio_plant_ch7_1946.mp4
    cc

But the files in :code:`cc` are named as such:

.. code:: shell

    SH-035-04-STR.xml
    SH-035-05-STR.xml
    SH-035-STR.xml
    SH-036-01-STR.xml
    SH-036-02-STR.xml
    SH-036-03-STR.xml
    SH-036-04-STR.xml
    SH-036-05-STR.xml
    SH-036-STR.xml
    SH-037-01-STR.xml
    SH-037-02-STR.xml
    SH-037-03-STR.xml
    SH-037-04-STR.xml
    SH-037-05-STR.xml
    SH-037-STR.xml

It's not possible to determine the related video asset from the closed captioning file itself.

.. code:: xml

    <?xml version="1.0" encoding="UTF-8"?>
    <tt xmlns="http://www.w3.org/2006/04/ttaf1" xmlns:tts="http://www.w3.org/2006/04/ttaf1#styling" xml:lang="en">
      <head>
        <styling>
          <style id="defaultSpeaker" tts:fontSize="24" tts:fontFamily="Arial" tts:fontWeight="normal" tts:fontStyle="normal" tts:textDecoration="none" tts:color="white" tts:backgroundColor="black" tts:textAlign="center" />
          <style id="defaultCaption" tts:fontSize="24" tts:fontFamily="Arial" tts:fontWeight="normal" tts:fontStyle="normal" tts:textDecoration="none" tts:color="white" tts:backgroundColor="black" tts:textAlign="center" />
        </styling>
      </head>
      <body style="defaultCaption" id="thebody">
        <div xml:lang="en">


Closed Captioning
-----------------

Closed captioning is provided in a variety of formats. The most common are:

* vtt
* xml (Timed Text Markup Language (TTML) format)
* txt (QTText)
* smil
* scc
* doc
* textClipping

Not all video assets have a closed captioning file associated with it.  It is unclear if this is because the vendor has
embedded the closed captioning in the video file or if the vendor has not provided closed captioning. More investigation
needs to be done to determine these cases. One approach might be to simply iterate over all the video files with ffmpeg:

.. code:: shell

    ffmpeg -i <video_file_path> -f lavfi -i "subtitles=fmt=srt" -map 0:v -map 1:s -c copy -f null -


File Formats
------------

The following file formats are used in the proprietary assets:

===
mp4
===

The vast majority of the proprietary assets have MP4 extensions. These 1162 files are either
:code:`Apple Lossless Codec (fmt/596)` or :code:`MPEG-4 Media Files (fmt/199)`. Further investigation needs to be
completed with Seigfried, Fido, or FFMPEG to determine the exact codecs used.

===
vtt
===

The most common subtitle file are vtts. 264 files are :code:`Web Video Text Tracks (WebVTT) Format (fmt/1454)` files.

===
xml
===

The next most common subtitle file is xml as Timed Text Markup Language (TTML) format.  224 files are
xml with a Timed Text Markup Language (TTML) Format DTD.

===
mov
===

There are also mov files. 19 files are either :code:`Apple ProRes (fmt/797)` or :code:`Quicktime (x-fmt/384)`. More
investigation should be done to determine more specific information such as codec. These are found in a variety of collections
but all found in a section called "testbed" (maybe they aren't used?).

===
mp3
===

There are a few mp3 files.  10 files are :code:`MPEG 1/2 Audio Layer 3 (fmt/134)` and are found in the "82" collection.

===
txt
===

There are 3 txt files that are used for closed captioning. They all appear to be QTText files.

===
m4v
===

There are 3 m4v files. They are all in the "instruction" collection and are :code:`MPEG-4 Media File (fmt/199)`.

====
smil
====

There are 2 video files in the pbs collection with :code:`Synchronized Multimedia Integration Language (Generic) (fmt/205)` caption files.

===
scc
===

There are 2 :code:`Sonic Scenarist Closed Caption Format (fmt/1274)` files used in the missmajor colleciton.

===
doc
===

There are 2 transcript files in the "transcripts" directory as doc files.  It's unclear how these are used.

============
textClipping
============

There is 1 "textClipping" file but it's empty.

===
3gp
===

There is 1 :code:`3GPP Audio/Video File (fmt/357)` file but it's in samples and appears to be unused.

