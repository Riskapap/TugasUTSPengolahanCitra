# Tugas UTS Pengolahan Citra
```
Riska Puspa Anggraeni Putri
TI.19.A2
311910440
```
## cara membuat citra berwarna (RGB) menjadi hitam putih (biner) menggunakan Graphical User Interface  (GUI) MATLAB
### langkah - langkah
1.  Membuka aplikasi software Matlab
![ScreenShot_20210428045213](https://user-images.githubusercontent.com/56241285/116317483-94bda680-a7dd-11eb-97a9-6b7c605937c4.png)
2. Membuka GUIDE Matlab dengan cara mengetik “guide” pada command window dan tekan enter
![1](https://user-images.githubusercontent.com/56241285/116317584-b6b72900-a7dd-11eb-9ec4-3946fd3fb5a5.png)
3. maka akan muncul seperti ini, Klik “Ok” pada GUIDE Quick Start >> Create New GUI >> Blank GUI (default) >> Save TugasGuiUTS
![2](https://user-images.githubusercontent.com/56241285/116317639-cd5d8000-a7dd-11eb-80c8-648f693bb627.png)
4. sehingga akan muncul tampilan GUIDE Matlab seperti pada gambar berikut
![3](https://user-images.githubusercontent.com/56241285/116317857-2200fb00-a7de-11eb-9e21-7f02ec7d4177.png)
5. Untuk menampilkan nama palet komponen, klik File >> Preferences
![4](https://user-images.githubusercontent.com/56241285/116318034-5b396b00-a7de-11eb-937b-346df3b651f5.png)
6. kemudian jangan beri tanda centang (√) pada menu Show File path in window title lalu klik “Ok”
![5](https://user-images.githubusercontent.com/56241285/116318461-00ecda00-a7df-11eb-9c83-735eba5db5b0.png)
7. Buatlah rancangan GUI MATLAB yang terdiri dari 4 axes, 1 pushbutton, 3  Radiobutton, dan 3 panel
![1](https://user-images.githubusercontent.com/56241285/116756736-cf6e4b80-aa36-11eb-8093-0f010a6360f3.png)
8. Editlah property masing-masing komponen dengan cara meng-double klik setiap komponen
- Pushbutton >> String = Open Image
![3](https://user-images.githubusercontent.com/56241285/116756858-13615080-aa37-11eb-8446-477ac42796ca.png)
- Radio Button 1 - 3 >> String = RGB, Grayscale, dan Binary
![5](https://user-images.githubusercontent.com/56241285/116756940-41469500-aa37-11eb-9c43-4d90c0697bf4.png)
- Panel >> String = Channel, Origibal Image, dan Complement Image
![6](https://user-images.githubusercontent.com/56241285/116757050-7b179b80-aa37-11eb-9258-e309ea63ee1a.png)
- Axes1 - Axes 4>> XTick = <kosongkan>, YTick = <kosongkan>, ZTick = <kosongkan>
![2](https://user-images.githubusercontent.com/56241285/116757080-91255c00-aa37-11eb-80e8-c3f00eea7d11.png)
9. maka tampilan GUI akan seperti ini
![1a](https://user-images.githubusercontent.com/56241285/116319932-86718980-a7e1-11eb-8409-5e5b4fa969cc.png)
10.  Listing Program untuk Open Image
![7](https://user-images.githubusercontent.com/56241285/116320064-c3d61700-a7e1-11eb-8a69-958c96fdba60.png)
lalu Masukan Kodingannya
  
```
% --- Executes on button press in pushbutton1.
function pushbutton1_Callback(hObject, eventdata, handles)
% hObject    handle to pushbutton1 (see GCBO)
% eventdata  reserved - to be defined in a future version of MATLAB
% handles    structure with handles and user data (see GUIDATA)
[name_file1,name_path1] = uigetfile( ...
    {'*.bmp;*.jpg;*.tif','Files of type (*.bmp,*.jpg,*.tif)';
    '*.bmp','File Bitmap (*.bmp)';...
    '*.jpg','File jpeg (*.jpg)';
    '*.tif','File Tif (*.tif)';
    '*.*','All Files (*.*)'},...
    'Open Image');
 
if ~isequal(name_file1,0)
    handles.data1 = imread(fullfile(name_path1,name_file1));
    guidata(hObject,handles);
    axes(handles.axes1);
    imshow(handles.data1);
else
    return;
end
```
11. Listing Program untuk konversi citra RGB menjadi grayscale
![8](https://user-images.githubusercontent.com/56241285/116320302-2af3cb80-a7e2-11eb-8775-b795a8888cc2.png)
lalu masukan kodingannya
```
% --- Executes on slider movement.
function slider1_Callback(hObject, eventdata, handles)
% hObject    handle to slider1 (see GCBO)
% eventdata  reserved - to be defined in a future version of MATLAB
% handles    structure with handles and user data (see GUIDATA)
 
% Hints: get(hObject,'Value') returns position of slider
%        get(hObject,'Min') and get(hObject,'Max') to determine range of slider
gray = handles.data2;
value = get(handles.slider1,'value');
thresh = imcomplement(im2bw(gray,value/255));
axes(handles.axes2);
imshow(thresh);
handles.data3 = thresh;
guidata(hObject,handles);
set(handles.edit1,'String',value)
```
12. Listing Program untuk menyimpan citra biner hasil konversi
![10](https://user-images.githubusercontent.com/56241285/116320440-727a5780-a7e2-11eb-8126-e7dec4757732.png)
masukan kodingan
```
% --- Executes on button press in pushbutton3.
function pushbutton3_Callback(hObject, eventdata, handles)
% hObject    handle to pushbutton3 (see GCBO)
% eventdata  reserved - to be defined in a future version of MATLAB
% handles    structure with handles and user data (see GUIDATA)
thresh = handles.data3;
[name_file_save,path_save] = uiputfile( ...
    {'*.bmp','File Bitmap (*.bmp)';...
    '*.jpg','File jpeg (*.jpg)';
    '*.tif','File Tif (*.tif)';
    '*.*','All Files (*.*)'},...
    'Save Image');
if ~isequal(name_file_save,0)
    imwrite(thresh,fullfile(path_save,name_file_save));
else
    return
end
```
13. Ketika di Run maka tampilan GUI akan tampak seperti ini
![11](https://user-images.githubusercontent.com/56241285/116320555-a0f83280-a7e2-11eb-9bd5-25c8079cc591.png)
14. Klik Open Image, pilih gambar yang ingin di masukan
![12](https://user-images.githubusercontent.com/56241285/116320589-b5d4c600-a7e2-11eb-9a5a-dbb21a032fcd.png)
15. Klik Grayscale
![13](https://user-images.githubusercontent.com/56241285/116320674-dc92fc80-a7e2-11eb-9823-7e491f59451e.png)
16. Geser nilai Slider
![14](https://user-images.githubusercontent.com/56241285/116320733-faf8f800-a7e2-11eb-8d94-fbd1b35c92d9.png)
17. Citra biner yang terbentuk dapat disimpan dengan cara meng-klik tombol Save
![15](https://user-images.githubusercontent.com/56241285/116320781-13691280-a7e3-11eb-9a86-8b1107fa52e1.png)
![16](https://user-images.githubusercontent.com/56241285/116320774-1106b880-a7e3-11eb-9f96-ae9c2357e502.png)
18. hasilnya
![17](https://user-images.githubusercontent.com/56241285/116320780-1237e580-a7e3-11eb-8f11-39de3ab702bd.png)
