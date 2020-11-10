# Apache-PDFBox-Example

### Encrypt PDF Document

```java

public static final String ENCRYPTED_PDF = "D://nonmember.pdf";

public final static String USER_PASSWORD = "password";
public final static String OWNER_PASSWORD = "user";


public static void main(String[] args) throws IOException {

   PDDocument document = null;

      try {

         document = PDDocument.load(new File(ENCRYPTED_PDF));

	 /** Setting access permissions */
	 AccessPermission permission = new AccessPermission();
	 permission.setCanPrint(false);
	 permission.setCanExtractContent(false);

	 StandardProtectionPolicy standardPP = new StandardProtectionPolicy(OWNER_PASSWORD, USER_PASSWORD, permission);
	 standardPP.setEncryptionKeyLength(128);
	 document.protect(standardPP);
	 document.save(ENCRYPTED_PDF);
	 document.close();

    } catch (IOException exception) {
	exception.printStackTrace();
	document.close();
    }
}   

```

### Reference

- https://memorynotfound.com/apache-pdfbox-encrypt-decrypt-pdf-document-java/
