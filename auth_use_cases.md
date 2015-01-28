Synthesized Requirements
========================

States of Authentication
------------------------

 * Anonymous
 * Clicked Through Interstitial
 * From IP Range / Institution
 * Authenticated User
     * From a Group of Users

Authorized Retrievals
---------------------

 * No image
 * Capped maximum size of full image
 * Restrict tiles to capped maximum of full image
 * Full image

 * No Manifest
 * Public Manifest
 * No AnnotationList
 * Public AnnotationList

Requested Features
------------------

 * Provide useful messages to the user
 * Provide link to where the user can authenticate
 * Describe auth requirements in Manifest/AnnoList
 * Use Sequence/Range to assign auth to all contained resources
 * Separate service to determine auth status

Use Cases
=========

* * * * *

Parker on the Web
-----------------

The "Parker on the Web" use-case - in which full access to image data is
available to subscribers and authenticated applications, and size-capped
access to the same image data is available to non-subscribers - is as
follows:

 * applies to image data only
 * authentication is handled by the app currently - the app has full
    access to all data, and subscribed users (from approved ip ranges)
    can access all content in full through the app; non-subscribed
    (anonymous) users can access a size-capped static image
 * desired state would be:
     * IIIF request from an authorized app or user would return up to full image, with all parameters enabled (rotate, etc.)
     * IIIF request from a non-auth'd app or user would return up to a specified zoom level
 * We specify rights at the object level for each object in the
    Stanford digital repository. The default "world" rights delivered by
    the server s/b be the capped image size; if the app or user is
    authenticated to the system, more becomes available.
 * If a non-auth'd app or user requests something larger than the
    capped size, would be nice to return the capped-size image and some
    sort of error message (ie. "subscription required for full access to
    this image").

* * * * *

Wellcome
--------

all extracted from
[https://gist.github.com/tomcrane/a1ef892b1fc5037c9f1b](https://www.google.com/url?q=https%3A%2F%2Fgist.github.com%2Ftomcrane%2Fa1ef892b1fc5037c9f1b&sa=D&sntz=1&usg=AFQjCNE2kRw-lPqa9Eravr1A6foZD1xQoA)

This is an implementation detail, for interest. The access condition
applied to any range must be one of:

 * Open
 * Requires Registration
 * Clinical Images
 * Library Staff
 * Restricted
 * Closed

Apart from "Open" they are really just arbitrary flags, so this section
is here to demonstrate Wellcome's particular auth implmentation.

All users of the site including unauthenticated users have permission to
see "Open" sections/ranges; most digitised books are "Open". The next
step up is "Requires Registration", which implies that the user has at
some point at least glanced at some terms and conditions and agreed to
them. Most archives are at this level because in the Wellcome Library's
case they are usually the personal letters of living (or more usually,
recently living) people.

There is no assumption about what "Requires Registration" actually
means, and in fact the Wellcome Library has recently changed the
behaviour here to encourage casual usage:

[http://wellcomelibrary.org/player/b20047459](http://www.google.com/url?q=http%3A%2F%2Fwellcomelibrary.org%2Fplayer%2Fb20047459&sa=D&sntz=1&usg=AFQjCNF_F-GtTLnrAefpSDtr7z7ffAmaNQ)

This used to present an unauthenticated user with a login prompt and
option to register (or log in via social media) including a "Ts & Cs"
checkbox at some point, but has been reduced to a "click-through"
acceptance of terms and conditions. Anything higher than "Requires
Registration" still prompts for login via a proper library account. This
new click-through still logs you in a special "guest" user, and creates
a cookie - that meant we didn't need to change the authentication module
that sits in front of the image servers and DDS servers (which provide
all the metadata).

Examples

The most common scenario, which applies to most digitised books, is that
the manifest contains a single sequence and that sequence has a simple
structure. The ranges identify front cover, title page etc, and all of
the ranges have the same access condition of "Open".

The next most common scenario applies to archives, where each manifest
has one sequence corresponding to a particular archival set of files.
These tend not to have any structure, because they are usually a group
of personal letters or files, so the structure has one range to which an
access condition of "Requires Registration" has been attached. This can
be seen in the example above. The table of contents is hidden because
there is no structure to display.

Almost all the material falls into one of the above categories. Here are
some other quirky scenarios:

[http://wellcomelibrary.org/player/b19813508](http://www.google.com/url?q=http%3A%2F%2Fwellcomelibrary.org%2Fplayer%2Fb19813508&sa=D&sntz=1&usg=AFQjCNGvds2BTqos_kTxBtQskuQxHl1gjw) -
The second image is restricted

[http://wellcomelibrary.org/player/b11607798](http://www.google.com/url?q=http%3A%2F%2Fwellcomelibrary.org%2Fplayer%2Fb11607798&sa=D&sntz=1&usg=AFQjCNHA_D5wDu7zh7g75VpR1BbMJQzMtw) -
the root section has the access condition "Clinical Images"

* * * * *

Artstor
-------

Artstor has both the open library and subscribed library. With
subscribed library, the access requires IP access or log in
authentication. We are planning to incorporate IIIF in the use cases for
subscribed member community, so that member can shared the collections.
But I am not too sure if it could be done at manifest level because it
does seems to be very complicated for user.

* * * * *

Yale
----

Yale's authentication use cases for the Image API align with those of
Stanford and ArtStor.   With regard to the Presentation API we'd want
the ability to control access to manifests and certainly need granular
control over annotations.  Notes below.

 * Images
    * Thumbnail if not authenticated
        * Our museums display  thumbnail images (limited by long edge pixel dimensions) of works which are under copyright or have restrictions placed upon them by donors. For the purposes of a course we would like to allow “full” size requests.
        * Equivalent to Stanford’s “Parker on the Web” use case
    * No image if not authenticated
        * Private faculty collections made available for a course
    * IP restriction [not an immediate use case for us]
        * Our rare books library restricts some materials to on-premise access only (IP restricted) due to (e.g.) donor restrictions.   This allows visiting researchers to access the materials without requiring a login account.

 * Presentation
    * Manifests
        * We’d like to restrict access to manifests (sequences, etc.) for certain projects. In the near term it’s likely that this would happen within the scope of a discrete project and we would be able to direct participants to the login page(s) for the relevant content.

    * Annotations
        * If annotations are retrieved from multiple endpoints we’d expect each to have its own auth service. I would expect a proliferation of services with ties to institutional services such as staff directories, LMS integration for teaching applications, custom databases for distributed research projects, etc.  

* * * * *

Harvard
-------

Image:

 * Need to determine from repository metadata whether image is public, restricted to Harvard, or non-displayable
     * In the future, we may have requirement for more granular restrictions (limited to reading room, limited to a set of individuals, limited to members of a course, etc.)
 * If restricted, need to be able to check an access cookie and grant  access if set
 * If cookie not set, need to redirect to an access management service which will determine whether the user is authorized or not
 * Need to be able to restrict or grant access based on ip address
 * Delivers thumbnails (full images \< 256 max dimension) regardless of access flag
 * Need to have global cap on max JPG image size delivered (currently 2048 long dimension)
 * Need to have custom settable max image dimension displayed on an image by image basis (some repositories have license agreements that restrict max image dimension to 600 pixels...)
     * Would like to optionally limit zooming and tile generation to prevent reconstruction

Presentation

 * Need global access flag (P, R, or N) for entire work's metadata, and
    individual setting per image as described above

* * * * *

Hill Museum & Manuscript Library (HMML)
---------------------------------------

At the Hill Museum & Manuscript Library (HMML), we utilize CONTENTdm as
our image repository server. Depending upon the collection, some images
are public and for some, users need to log in to CONTENTdm as a user
with those permissions to see the collection. Permissions are granted on
a user by user basis through our IT Department.

The other way that users will be able to see images that are in a locked
down collection is through our vHMML system (still in development).
VHMML uses API calls to CONTENTdm.

For example,

[http://cdm.csbsju.edu/utils/ajaxhelper/?CISOROOT=SGD&CISOPTR=4697&action=2&DMSCALE=90&DMWIDTH=4000&DMHEIGHT=2733&DMX=0&DMY=0&DMTEXT=text&DMROTATE=0](http://www.google.com/url?q=http%3A%2F%2Fcdm.csbsju.edu%2Futils%2Fajaxhelper%2F%3FCISOROOT%3DSGD%26CISOPTR%3D4697%26action%3D2%26DMSCALE%3D90%26DMWIDTH%3D4000%26DMHEIGHT%3D2733%26DMX%3D0%26DMY%3D0%26DMTEXT%3Dtext%26DMROTATE%3D0&sa=D&sntz=1&usg=AFQjCNGZHFk0CL0UwaEynPjZvjpIWWx9ow)

* * * * *

National Library of Wales
-------------------------

Rights for image data only not metadata:

Wills Images - We sell digital copies of these so free public access
should be to a low quality version. After purchase system should supply
a username + password to get to the full quality copy - similar to
‘Parker on the Web use case’

Internal Only - Some images are accessible internally to the library
only authenticated with IP address

We have sort permission to display an image on a particular website but
a user shouldn’t download it for their own uses. This could be some sort
of ‘authorised app’ or just a clear presentation of license terms.

NLW would also be interested in exploring cookies as a way to store the
fact that authentication has occurred and doesn’t need to be redone for
a period of time. It should speed up tile access as the authentication
only happens on the first request. The cookie would have to be encrypted
and time bound in some way that couldn’t be faked.

* * * * *
