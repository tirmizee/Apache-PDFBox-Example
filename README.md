# Apache-PDFBox-Example

### Encrypt PDF Document With File

<b>

```java

public static final String ENCRYPTED_PDF = "D://nonmember.pdf";

public final static String USER_PASSWORD = "password";
public final static String OWNER_PASSWORD = "user";


public static void main(String[] args) throws IOException {

     try (PDDocument document = PDDocument.load(new File(ENCRYPTED_PDF))) {

	 /** Setting access permissions */
	 AccessPermission permission = new AccessPermission();
	 permission.setCanPrint(false);          // ไม่สามารถสั่งปริ้นได้
	 permission.setCanExtractContent(false); // ไม่สามารถ...

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

</b>

#### Encrypt PDF Document With Btyes

<b>

```java

    public static byte[] encryptWithPassword(byte[] bytes, String password, int length) throws IOException {
        try (PDDocument document = PDDocument.load(bytes)) {
	    AccessPermission permission = new AccessPermission();
	    StandardProtectionPolicy standardPP = new StandardProtectionPolicy(password, password, permission);
	    standardPP.setEncryptionKeyLength(length);
	    document.protect(standardPP);
	    ByteArrayOutputStream outputStream = new ByteArrayOutputStream();
	    document.save(outputStream);
	    return outputStream.toByteArray();
	}
    }

```

#### Encrypt PDF Document With InputStream

<b>

```java

    public static byte[] encryptWithPassword(InputStream stream, String password, int length) throws IOException {
	try (PDDocument document = PDDocument.load(stream)) {
            AccessPermission permission = new AccessPermission();
            StandardProtectionPolicy standardPP = new StandardProtectionPolicy(password, password, permission);
            standardPP.setEncryptionKeyLength(length);
            document.protect(standardPP);
            ByteArrayOutputStream outputStream = new ByteArrayOutputStream();
            document.save(outputStream);
            return outputStream.toByteArray();
        }
    }

```

</b>

#### Decrypt PDF Document

<b>

```java

    public static final String ENCRYPTED_PDF = "D://nonmember.pdf";

    public final static String USER_PASSWORD = "password";
    public final static String OWNER_PASSWORD = "user";
	
    public static void main(String[] args) throws Exception{

        try (PDDocument document = PDDocument.load(new File(ENCRYPTED_PDF), USER_PASSWORD)) {
	    document.setAllSecurityToBeRemoved(true);
	    document.save(ENCRYPTED_PDF);
        } catch (IOException e){
            System.err.println("Exception while trying to read pdf document - " + e);
        }
    }


```

</b>

### Reference

- https://memorynotfound.com/apache-pdfbox-encrypt-decrypt-pdf-document-java/
