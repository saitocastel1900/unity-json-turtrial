# unity-json-turtrial
This is the project when learning about Json.

## What' Json(JavaScript Object Notation)
・Files similar to C# dictionaries, with a method of managing data by name and key.  
・To use Json on Unity, you need to use the JsonUtility provided by Unity.  
・Javascript originated  
・Often used in unity with save functions.  

```
{
//Tie the name and value to each other.
"name": "Makaroni",
"velocity": 12.5,
"isFlag": true,
}  

//Can be managed in arrays.
{
  "Userinfo": [
    {
      "id": 1,
      "name": "saito",
      "isHuman": true
    },
    {
      "id": 2,
      "name": "takahashi",
      "isHuman": false
    },
    {
      "id": 3,
      "name": "monaka",
      "isHuman": false
    }
  ]
}
```

## What's JsonUtility  
・Simple structure with only three functions.  
>1. JsonUtility.FromJson //Converting Json data to Unity objects.
>2. JsonUtility.FromJsonOverwrite //overwrite function
>3. JsonUtility.ToJson()  //Converting Unity objects to Json data.
### FromJson Instantiate (Json data)
```
//JSON -> Instance
//Read Json data in the Resources folder.
 string json = Resources.Load<TextAsset>("Data1").ToString();
       
 //Instantiate the data read in.
 Data01 data01 = JsonUtility.FromJson<Data01>(json);
 
 Debug.Log("name:"+data01.player[0].name+" age:"+data01.player[0].playerinfo.age);
```
### FromJsonOverwrite (Overwrite Json data with other Json data)
```
//(JSON,Instance)
//JSON -> Instance
JsonUtility.FromJsonOverwrite(data01toJson, data02toJson);
Debug.Log(data02toJson);
```
### ToJson (Convert instances to Json data)
```
//Instance -> JSON
string data01toJson = JsonUtility.ToJson(data01).ToString();
Debug.Log(Data01toJson);
```
## Json-based save system
**・PlayerPrefs is not used.**  
**・FromJsonOverwrite is not used, StreamWriter is used**
**・Use singletons because you want to share values across scenes**

### Important methods that were not introduced
・File.WriteAllText(path, fileName) //Exporting files  
・StreamReader streamReader = new StreamReader (filePath, character code) //Read file   
 streamReader.WriteLine(string)  
・StreamWriter streamWriter = new StreamWriter (filePath, append : true) //Exporting files
### SaveManager.cs
#### Save()
・Method to write the data to be saved to a Json file.
#### Load()
・Methods to read data from Json files present in the Asset folder.
### Data.cs
・Register the value you want to keep as Public.  
・[System.Serializable] needs to be attached to the class as it is required for converting instances to Json.  
```
[Serializable]
    public class Data
    {
        public string name = "DefaultName";
        public int id = -1 ;
    }
```
![diagram-7813544578852950416](https://user-images.githubusercontent.com/96648305/163936045-64be4d55-9fc8-4f19-9870-0aff2c2c755d.png)

*Saved data must be encrypted to prevent misuse by users(The way to do it is through binaries and so on.).

### Try encrypting Json data
There are many different encryption methods, but this section introduces the use of XOR(The most famous encryption is the use of binaries and so on).  

# Reference document
https://kan-kikuchi.hatenablog.com/entry/JsonUtility  
https://www.hanachiru-blog.com/entry/2019/04/24/211642  
https://docs.unity3d.com/ja/2018.4/ScriptReference/JsonUtility.html  
https://kurokumasoft.com/2022/01/03/unity-savesystem-using-json/  
https://www.youtube.com/watch?v=MZAU7HW4S8Q  
https://www.slideshare.net/torisoup/unityzenject
