
Origami
=====

Overview
--------

This is a fork of the [original origami project](https://github.com/gdelugre/origami). 

I have added a way to sign PDF files with an external provider, such as the Austrian "[Handy-Signatur](http://handy-signatur.at)" (Mobile Phone Signature)

Currently only PDF PKCS#7 signatures are supported, however I plan to support PAdES (PDF Advanced Electronic Signatures) as well.

Requirements
-------

You can review requirements and other important information at the [original origami project](https://github.com/gdelugre/origami).

Quickstart
-------

This fork adds two new methods for PDF manipulating.

    base64_string = pdf.prepare_signature(
          name: "John Doe",
          location: "Somewhere",
          contact: "john@doe.com",
          reason: "PDF Signature Test",
          method: Signature::PKCS7_DETACHED,
          content_size: 4096)

`prepare_signature`  adds the signature object to the PDF document and prepares it for signing. You can specify some parameters which are shown when opening the PDF with a PDF reader (name, location, etc). This method returns the PDF as a Base64 encoded string, excluding the signature placeholder.

    insert_signature(signature_base64)

This method inserts the signature back into the PDF (at the /Content object).

Code example [here](examples/signature/external_signature.rb).

Flow
-------

 1. Read or create PDF document
 2. Prepare the signature
 3. Send Base64 content to external signature provider
 4. Insert the signature into the PDF
 5. Finish

Known Bugs
-------

When saving the PDF after preparing it and re-reading it from disk, the Signature Object can get scrambled up, which invalidates the ByteRange array and also the signature.

Helpful Literature
-------

[Digital Signatures in a PDF](https://www.adobe.com/devnet-docs/acrobatetk/tools/DigSig/Acrobat_DigitalSignatures_in_PDF.pdf)

[Portable Document Format Reference Manual Version 1.3](https://www.pdfill.com/download/PDFSPEC13.pdf)

License
-------

Origami is distributed under the [LGPL](COPYING.LESSER) license.

Copyright © 2017 Guillaume Delugré.
