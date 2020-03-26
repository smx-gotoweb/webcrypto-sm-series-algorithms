# Security and Privacy self-review

This has been created by cut-and-paste from https://w3ctag.github.io/security-questionnaire/.

1. **What information might this feature expose to Web sites or other parties, and for what purposes is that exposure necessary?**

   This feature exposes opaque key handles in the form of CryptoKey or various formats of serialized key or key materials. The above exposure is part of the current WebCrypto spec to provide useful but subtle crypto primitives.

2. **Is this specification exposing the minimum amount of  information necessary to power the feature?**

   YES, as explained for the previous question.

3. **How does this specification deal with personal  information or personally-identifiable information or information derived  thereof?**

4. **How does this specification deal with sensitive  information?**

   For the above two questions, please refer to the current WebCrypto spec for this aspect, since this feature does not introduce new ways of handling such information.

5. **Does this specification introduce new state for an origin that persists across browsing sessions?**

   No.

6. **What information from the underlying platform, e.g. configuration data, is exposed by this specification to an origin?**

   Pre-shared key or key material can be serialized and exposed to an origin by operations that are currently specified by WebCrypto, and this feature supports these operations. In order to achieve this feature, we need to add some additional parameters to support it such as  "Sm4CbcParams" , "Sm4CbcParams", and "Sm2KeyGenParams"  mentioned in "explain.md" document.

7. **Does this specification allow an origin access to sensors on a user’s device?**

   No.

8. **What data does this specification expose to an origin?  Please also document what data is identical to data exposed by other features, in the same or different contexts.**

   This feature exposes the same types of data as in the supported operations in the current WebCrypto spec.

9. **Does this specification enable new script  execution/loading mechanisms?**

   No.

10. **Does this specification allow an origin to access  other devices?**

    No.

11. **Does this specification allow an origin some measure  of control over a user agent’s native UI?**

    No.

12. **What temporary identifiers might this specification  create or expose to the web?**

    This feature does create or expose data that can be used as temporary identifiers.

13. **How does this specification distinguish between behavior in first-party and third-party contexts?**

    This feature does not distinguish between these contexts.

14. **How does this specification work in the context of a user agent’s Private Browsing or "incognito" mode?**

    This feature does not distinguish between these modes.

15. **Does this specification have a "Security Considerations" and "Privacy Considerations" section?**

    YES.

16. **Does this specification allow downgrading default  security characteristics?**

    NO.

 