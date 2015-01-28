IIIF Authentication Working Group Charter

# Current Members:

* Rob Sanderson (Stanford)

* Jon Stroop (Princeton)

* Simeon Warner (Cornell)

* Tom Crane (Digirati)

* Michael Appleby (Yale)

# Summary of Work:

The Authentication Working Group is chartered to design, specify and implement a viable solution to authentication and authorization for the IIIF APIs.  The primary deliverable is a specification for an interoperable pattern that client and server systems can implement to allow users to use arbitrary authentication systems as needed in order to receive the authorization credentials required to interact with image content.  Secondary to this is the application of the pattern to the Presentation API, and best practices for the linking from Presentation API to authentication required image resources.

# Community Need Established:

At the London October 2014 meeting, almost all of the participating institutions stated a need for a shared system that enabled authentication and authorization for image content.   Participating institutions that did not have the need (e-codices, Europeana, Biblissima) recognised the importance of the work.  It was ranked as the highest priority for work in the 12 months following the meeting by those present. 

The meeting notes were subsequently circulated on the IIIF-Discuss list.  The standing IIIF Editorial board were all present at the discussion and unanimously agreed that technical work should commence.

# Communication Channels:

All of the work will be performed in publicly accessible spaces:

* IIIF-Discuss will be the primary communication channel, with messages prefixed by "[auth]"

* Implementations will be shared and made available in a github repository:*[https://github.com/IIIF/aut*h](https://github.com/IIIF/auth)

* Issues for implementations and the specifications will be tracked via the github repository issue list:*[https://github.com/IIIF/auth/issue*s](https://github.com/IIIF/auth/issues)

* Collaborative documents will be shared and edited via Google Docs, in the folder:*[http://goo.gl/0BjDO*x](http://goo.gl/0BjDOx)

# Known Initial Requirements:

* Authentication system must not require direct interaction of the IIIF client, as institutions have many and varied requirements and implementations.  Clients may not be able to access the response from the authentication system as to whether the user successfully logged in or not, if it is from a third party system like OAuth.

* Degraded images must be possible using the designed system, whereby unauthorized users can still get image content, but in a degraded experience.  Degradation options include watermarking, lower maximum resolution, lower maximum quality, amongst others.  Describing the exact nature of the degradation is not in scope.

* Authentication described as a service that can be associated with different resources, and listed as a supported feature in the Image Information response.

# Deliverables:

* Use Case description and analysis document

* Image API Authentication specification document

    * How image content served via the IIIF Image API can be protected using authentication/authorization techniques

* Presentation API Authentication specification document

    * How Manifests and other Presentation API content can be protected using authentication/authorization techniques

    * N.B. This may be the same document as above	

* Proposal for Presentation API advertising of Image authentication

    * How the Presentation API can describe Image Authentication requirements; this may require additional experimentation, use case collection and development effort

* Reference implementation of conforming server

* Reference implementation of conforming client

The specifications will be initially developed as an annex to the current 2.0 documents, and may be incorporated into future versions of the core specifications.  It is believed that none of the current functionality needs to be changed, and that the authentication features are orthogonal to existing features.

# Timeline:

* February 2015: Face to Face at LDCX, Stanford

* March-April 2015: Experimental implementation and draft specification, use case document

* May 2015: Presentation of drafts at D.C. Meeting

* June: Revision of specification and implementation from IIIF feedback

* July: Face to Face, Presentation at Open Repositories, community feedback solicited

* August-September: Revision of specification and implementation from community feedback

* October: Presentation of final draft specification at [Europe] Meeting

* November-December: Final revisions and broad last call for feedback

* January 2015:  Publication of Specifications and reference implementations; call for implementations

# Meeting Time Requested:

* May 2015:  2 hours plenary, 6 hours WG

* October 2015: 2 hours plenary, 2 hours WG

# **Adoption Strategy:**

Known Products:

* Loris: Stroop/community to do Summer 2014

* IIIP:   Can we get Ruven into the WG?

* Mirador: Winget,Sanderson to do Summer 2104

* Wellcome: Digirati to do ???

* Djatoka shim: ???

* FSI shim: ???

