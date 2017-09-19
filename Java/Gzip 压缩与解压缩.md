## Gzip 压缩与解压缩

#### 压缩

```java
    public static byte[] gzip(byte[] data) {
        try {
            ByteArrayOutputStream bos  = new ByteArrayOutputStream();
            GZIPOutputStream      gzip = new GZIPOutputStream(bos);
            gzip.write(data);
            gzip.finish();
            gzip.close();
            byte[] bytes = bos.toByteArray();
            bos.close();
            return bytes;
        } catch (IOException e) {
            e.printStackTrace();
        }
        return null;
    }
```

#### 解压缩

```java
    public static byte[] ungzip(byte[] data) {
        try {
            ByteArrayInputStream  bis  = new ByteArrayInputStream(data);
            GZIPInputStream       gzip = new GZIPInputStream(bis);
            byte[]                bytes  = new byte[1024];
            int                   len;
            ByteArrayOutputStream bos  = new ByteArrayOutputStream();
            while ((len = gzip.read(bytes, 0, bytes.length)) != -1) {
                bos.write(bytes, 0, len);
            }
            gzip.close();
            bis.close();
            byte[] byteArray = bos.toByteArray();
            bos.flush();
            bos.close();
            return byteArray;
        } catch (IOException e) {
            e.printStackTrace();
        }
        return null;
    }
```

