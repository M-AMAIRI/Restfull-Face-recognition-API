

# Face recognition Restful API Description

Requiperent : 
  - Ubuntu 16.04
  - docker 
  - pip python
  - curl
# internal code architecture

 * [Python_mainApp.py](./tree-md)
 * [models.py](./dir2)
 * [Images](./dir1)
   * [Id_Person_1.jpg](./dir1/file11.ext)
   * [Id_Person_2.jpg](./dir1/file12.ext)
   * [Id_Person_1.jpg](./dir1/file11.ext)
   *  . . .
 * [Data](./file_in_root.ext)
   * [LandMarker_Person-1.dat](./dir1/file11.ext)
   * [LandMarker_Person-2.dat](./dir1/file11.ext)
   * [LandMarker_Person-3.dat](./dir1/file11.ext)
   * . . .
 * [README.md](./README.md)

- at the start of the application the folders **Images** and **Data** will be created automatically .
- models.py an interface created to access the data models ( trained data .dat files ) .

# Installation :

  - python dependency installation 
```sh
$ pip install -r requirements.txt
```
> Install dependencies directly from requirements.txt
> in pip installation

after installing the dependencies, launch the application directly with this command:

```sh
$ python Python_mainApp.py

  * Restarting with stat
  * Debugger is active!
  * Debugger PIN: 118-167-610
  * Running on http://0.0.0.0:5001/ (Press CTRL+C to quit)
```
And then once this command is launched, the service will be ready to use

### How to use this service

Open another terminal and Run a curl post command , and here an example of the control :

```sh
$ curl -XPOST -F cmd=TrainNew/Retrain/Recognition -F ID=moatez54 -F "file=@image.jpg" http://127.0.0.1:5001
```

| Parametre | Description |
| ------ | ------ |
| PWD | Putting a password in the API call , **MAMAIRI** by default |
| CMD | the goal of query : **Recog** , **DELT** or **Train**  |
| ID | the **id** of the person in the case of system training  |
| file | the name of the image file to pass as parameter it can be **.jpg** or **.png**  |

test case :

- in case if we miss to add the Password argument to the command 
```sh
curl -XPOST -F cmd=TrainNew/Retrain/Recognition -F ID=moatez54 -F "file=@Saber.jpg" http://127.0.0.1:5001
```
request :
```sh
{
  "Status": "password does not match"
}
```

- in case the command **CMD** is not recognized
```sh
{
  "Status": "No command Selected Please choose one of them DELT,Recog or Train "
}
```

- train new Id , and adding new person to database :
```sh
curl -XPOST -F CMD=Train -F PWD=MAMAIRI -F ID=moatez54 -F "file=@Saber.jpg" http://127.0.0.1:5001
```
request :
```sh
{
  "Process": "Training",
  "Result": "process succeeded",
  "Status": "New Person ID"
}
```
- post command for facial recognition from an image :
```sh
curl -XPOST -F CMD=Recog -F PWD=MAMAIRI -F "file=@Image1.jpg" http://127.0.0.1:5001
```
```sh
{
  "Process": "Recog",
  "Result": "Saber,",
  "Status": "Satus of recognition"
}
```

- to delete a specific id from database :
```sh
$curl -XPOST -F CMD=DELT -F PWD=MAMAIRI -F ID=Saber -F "file=@Image1.jpg" http://127.0.0.1:5001
```
```sh
{
  "ID": "Saber",
  "Process": "Delete",
  "Status": "Id : Saber have been deleted from database"
}
```




Version beta ,


