Portable House Data Metadata
============================

The metadata section is designed to contain information about the source of the data, request and client information, version information, and timestamps.

The object key for this section is ``metadata``.

Compatibility
*************

Document last updated for schema version *v1.0.1*


Schema Version (REQUIRED)
**********************************

The object key for this section is ``schemaVersion``.

  ==================================  ========  =======  ===========  ========  ===========  ============================================================
  Variable Name                       Type      Units    Constraints  Required  Default      Notes
  ==================================  ========  =======  ===========  ========  ===========  ============================================================
  ``schemaVersion``                   string                          Yes                    Version in format `v*.*.*`
  ==================================  ========  =======  ===========  ========  ===========  ============================================================


Client Information
**********************************

Those leveraging the portable house data format should ensure that they have recieved explicit permission from their clients before sharing their name and contact information with other parties.

The object key for this section is ``client``.

  ==================================  ========  =======  ===========  ========  ===========  ============================================================
  Variable Name                       Type      Units    Constraints  Required  Default      Notes
  ==================================  ========  =======  ===========  ========  ===========  ============================================================      
  ``clientFirstName``                 string                          No                     Client first name
  ``clientLastName``                  string                          No                     Client last name
  ``clientEmail``                     string                          No                     Client email address
  ``clientId``                        string                          No                     Unique ID for the client (i.e. for platforms to reference)
  ``clientRequestInfo``               string                          No                     Details about the client's request
  ==================================  ========  =======  ===========  ========  ===========  ============================================================


Request (REQUIRED)
**********************************
Information representing the request (i.e. the action of sharing the portable house data information via an API)

The object key for this section is ``request``.

  ==================================  ========  =======  ===========  ========  ===========  ============================================================
  Variable Name                       Type      Units    Constraints  Required  Default      Notes
  ==================================  ========  =======  ===========  ========  ===========  ============================================================      
  ``requestID``                       string                          Yes                    Unique ID for the request (e.g. UUID)
  ``requestTimeStamp``                string                          Yes                    Timestamp for the request
  ==================================  ========  =======  ===========  ========  ===========  ============================================================

Service Provider (REQUIRED)
**********************************
Information representing the agent making the request.

The object key for this section is ``serviceProvider``.

  ==================================  ========  =======  ===========  ========  ===========  ============================================================
  Variable Name                       Type      Units    Constraints  Required  Default      Notes
  ==================================  ========  =======  ===========  ========  ===========  ============================================================      
  ``providerName``                    string                          Yes                    Provider name
  ``providerEmail``                   string                          No                     Provider contact email
  ``providerId``                      string                          Yes                    Unique ID for the request (e.g. UUID)
  ==================================  ========  =======  ===========  ========  ===========  ============================================================


