:original_name: obs_21_2119.html

.. _obs_21_2119:

How Do I Generate an SSE-C Encryption Key?
==========================================

Sample code of generating an SSE-C encryption key and its MD5 value:

::

   import java.nio.charset.Charset;
   import java.security.MessageDigest;
   import java.security.NoSuchAlgorithmException;

   public class SseCTool {
       public static void main(String[] args) {
           // Below is an encryption key example. The key can be changed as needed, but it must be 32 characters long (a 256-bit string).
           String keyString = System.getenv("ACCESS_KEY_ID");
           // Compute the x-obs-server-side-encryption-customer-key header.
           String customerKey = toBase64String(keyString.getBytes(Charset.forName("UTF-8")));
           System.out.println("customer key is : " + customerKey);

           // Compute the x-obs-server-side-encryption-customer-key-MD5 header.
           String customerKeyMD5 = computeMD5(fromBase64(customerKey));
           System.out.println("md5 for customer key is : " + customerKeyMD5);
       }

       // Compute the Base64 character string.
       public static String toBase64String(byte[] data) {
           java.util.Base64.Encoder encoder = java.util.Base64.getEncoder();
           return new String(encoder.encode(data), Charset.forName("UTF-8"));
       }

       // Compute the MD5 character string.
       public static String computeMD5(byte[] b64Data) {
           try {
               MessageDigest md5 = MessageDigest.getInstance("MD5");
               md5.update(b64Data);

               byte[] byteArray = md5.digest();

               return toBase64String(byteArray);
           } catch (NoSuchAlgorithmException e) {
               e.printStackTrace();
               return "";
           }

       }

       public static byte[] fromBase64(String b64Data) {
           java.util.Base64.Decoder decoder = java.util.Base64.getDecoder();
           return decoder.decode(b64Data.getBytes(Charset.forName("UTF-8")));
       }
   }
