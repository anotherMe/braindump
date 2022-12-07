
A rudimentary method to access files from the *resources* folder:


```java
/**
     *
     * @param pathToResource - a String like "src/test/resources/my_fancy_file.name"
     * @return
     * @throws Exception
     */
    public byte[] readXMLToByteArray(String pathToResource) throws Exception {

        File file = new File(pathToResource);
        FileInputStream fl = new FileInputStream(file);
        byte[] arr = new byte[(int)file.length()];
        fl.read(arr);
        fl.close();
        return arr;
    }
    
```