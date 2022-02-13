
#include<iostream>
#include<string>
#include<vector>
using namespace std;
//Url class
class URL {
private:
    string scheme;
    string authority;
    string path;
public:
    URL(string url) {
        int firstColonIndex = url.find(":");
        scheme = url.substr(0, firstColonIndex);
        string restUrl = url.substr(firstColonIndex + 3, url.length());
        int thirdSlashIndex = restUrl.find("/");
        authority = url.substr(firstColonIndex + 3, thirdSlashIndex);
        path = restUrl.substr(thirdSlashIndex, url.length());
    }

    string getScheme() {
        return scheme;
    }

    string getAuthority() {
        return authority;
    }

    string getPath() {
        return path;
    }

    string getCompleteURL() {
        return scheme + "://" + authority + path;
    }
};
class ImageMetaData{ //class declaration
private: //all the private members
    string fileName;
    string imageType;
    int dd,mm,yy;
    double size;
    string authorName;
    double width,height;
    string apertureSize;
    double exposureTime;
    int iso;
    bool flash;
public:
    string getFileName(){
        return fileName;
    }
    void setFileName(string name){
        fileName=name;
    }
    string getImageType(){
        return imageType;
    }
    void setImageType(string type){
        if(type=="PNG" || type=="GIF" || type=="JPEG")
            imageType=type;
        else
            cout<<type<<" : Image Type Not Supported"<<endl;
    }
    int getDay(){
        return dd;
    }
    int getMonth(){
        return mm;
    }
    int getYear(){
        return yy;
    }
    void setDate(int d,int m,int y){
        if(d>0 && d<32 && m>0 && m<13 && y>0){
            dd=d;mm=m;yy=y;
        }
        else
            cout<<"Invalid Date"<<endl;
    }
    double getSize(){
        return size;
    }
    void setSize(double s){
        if(s>=0)//size can not be -ve
            size=s;
        else
            cout<<"Invalid Size"<<endl;
    }
    string getAuthorName(){
        return authorName;
    }
    void setAuthorName(string name){
        authorName=name;
    }
    void setDimensions(double w,double h){
        if(w>=0 && h>=0){
            width=w;
            height=h;
        }
        else{
            cout<<"Invalid Dimensions"<<endl;
        }
    }
    double getWidth(){
        return width;
    }
    double getHeight(){
        return height;
    }
    string getApertureSize(){
        return apertureSize;
    }
    void setApertureSize(string aSize){
        if(aSize.size()>2 && aSize.at(0)=='f' && aSize.at(1)=='/')
            apertureSize=aSize;
        else
            cout<<"Invalid Aperture Size format"<<endl;
    }
    void setExposureTime(double eTime){
        if(eTime>=0)
            exposureTime=eTime;
        else
            cout<<"Invalid ExposureTime Format"<<endl;
    }
    double getExposureTime(){
        return exposureTime;
    }
    void setISO(int ISO){
        iso=ISO;
    }
    int getISO(){
        return iso;
    }
    void setFlash(bool enabled){
        flash=enabled;
    }
    bool isFlashEnabled(){
        return flash;
    }
};

//print the instance variable of metadata object
void print(ImageMetaData metaData){
    cout<<"Print the image metadata"<<endl;
    cout<<"File Name : "<<metaData.getFileName()<<endl;
    cout<<"Image Type : "<<metaData.getImageType()<<endl;
    cout<<"Creation Date : "<<metaData.getDay()<<"/"<<metaData.getMonth()<<"/"<<metaData.getYear()<<endl;
    cout<<"Image Size : "<<metaData.getSize()<<endl;
    cout<<"Author Name : "<<metaData.getAuthorName()<<endl;
    cout<<"Image Dimension : "<<metaData.getWidth()<<"x"<<metaData.getHeight()<<endl;
    cout<<"Aperture Size : "<<metaData.getApertureSize()<<endl;
    cout<<"Exposure Time : "<<metaData.getExposureTime()<<endl;
    cout<<"ISO Value : "<<metaData.getISO()<<endl;
    cout<<"Flash Enabled : "<<metaData.isFlashEnabled()<<endl;
    cout<<endl;
}
//Item class
class Item
{
public:

    string name;
    long id;
    double price;
    int stock;

};
//Store class
class Store
{
public:

    vector<Item> item_list;

    void print_item_list()
    {
        if(item_list.empty())
        {
            cout<<"\nItem List is Empty !!!";
            return;
        }

        cout<<"Store:"<<endl;

        for(Item i : item_list)
        {
            cout<<i.name<<" x "<<i.stock<<endl;
        }
        return;
    }

    void add_item(Item s)
    {
        item_list.push_back(s);

        return;
    }
};
int main() {

    URL u("https://www.blessing.com/new/posts");
    cout << "Scheme: " << u.getScheme() << endl;
    cout << "Authority: " << u.getAuthority() << endl;
    cout << "Path: " << u.getPath() << endl;
    cout << "Complete URL: " << u.getCompleteURL() << endl;

    ImageMetaData metaData;
    metaData.setFileName("Billy");
    metaData.setImageType("PNG");
    metaData.setDate(01,01,2022);
    metaData.setSize(35);
    metaData.setAuthorName("Blessing");
    metaData.setDimensions(25,35);
    metaData.setApertureSize("f/8");
    metaData.setExposureTime(1.0/1000.0);
    metaData.setISO(600);
    metaData.setFlash(true);
    print(metaData);
    Item i;
    i.name="Book";
    i.id=101;
    i.stock=12;
    i.price=12.0;

    Item it;
    it.name="Colored Pencils";
    it.id=102;
    it.stock=15;
    it.price=20.0;

    Store store;
    store.add_item(i);
    store.add_item(it);

    store.print_item_list();



    return 0;

}
