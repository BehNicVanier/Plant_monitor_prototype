#include <iostream>
#include <stdlib.h>
#include <cstdlib>
using namespace std;
/*this is a prototype of the system of the arduino plant monitor
current procedure:
	-displays a false value which represents thre value retrieved from the sensor
	-displays the value for one of the folowing graphs (max value)
	-
*/
int main (){
	//Variables used
	float ihum, itemp[3], imos;				//variables for the sensor values retrieved from all of the sensors
	float ihummax=0, itempmax=0, imosmax=0;	//used to determine the max value of the sensor values
	float ihum_req, imos_req;				//used to send error message if there is a spec of the living condiion of the plant which is not met
	int iselect;							//used for desicion making
	int icount;								//variable for cunter loop 
	/*concept of itemp as an array
	the plant will have a temperature with a range. This range will be from itemp[1] to itemp[2] degrees celsius.
	itemp[3] will be the value from the sensor]*/										
	cout << "Select the type of plant" << endl;
	//list of 10 options (9 plants and 1 alternate)
	cout << "1: Aloe Vera" << endl;
	cout << "2: Rose" << endl;
	cout << "3: Tomato" << endl;
	cout << "4: Spider plant" << endl;
	cout << "5: Snake plant" << endl;
	cout << "6: English Ivy" << endl;
	cout << "7: Cast iron plant" << endl;
	cout << "8: Sunflower" << endl;
	cout << "9: Dill plant" << endl;
	cout << "10: My plant is not in the following list" << endl;
	cin >> iselect;			//Selecting the following inputs
	cout << endl;
	switch(iselect){
		case 1:		//aloe vera
			itemp[1] = 13;	//temp range
			itemp[2] = 27;
			ihum_req = 375;		//humidity (measured in ppm)
			imos_req = 0.15;	//moisture (%)
		case 2:		//rose
			itemp[1] = 18;	//temp range
			itemp[2] = 25;
			ihum_req = 375;		//humidity (measured in ppm)
			imos_req = 0.15;	//moisture (%)
		case 3:		//tomato plant
			itemp[1] = 20;	//temp range
			itemp[2] = 27;
			ihum_req = 375;		//humidity (measured in ppm)
			imos_req = 0.15;	//moisture (%)
		case 4:		//spider plant
			itemp[1] = 18;	//temp range
			itemp[2] = 24;
			ihum_req = 375;		//humidity (measured in ppm)
			imos_req = 0.15;	//moisture (%)
		case 5:		//snake plant
			itemp[1] = 26;	//temp range
			itemp[2] = 30;
			ihum_req = 375;		//humidity (measured in ppm)
			imos_req = 0.15;	//moisture (%)
		case 6:		//english ivy
			itemp[1] = 13;	//temp range
			itemp[2] = 21;
			ihum_req = 375;		//humidity (measured in ppm)
			imos_req = 0.15;	//moisture (%)
		case 7:		//cast iron plant
			itemp[1] = 7;	//temp range
			itemp[2] = 30;
			ihum_req = 375;		//humidity (measured in ppm)
			imos_req = 0.15;	//moisture (%)
		case 8:		//sunflower
			itemp[1] = 13;	//temp range
			itemp[2] = 16;
			ihum_req = 375;		//humidity (measured in ppm)
			imos_req = 0.15;	//moisture (%)
		case 9:		//dill plant
			itemp[1] = 15;	//temp range
			itemp[2] = 21;
			ihum_req = 375;		//humidity (measured in ppm)
			imos_req = 0.15;	//moisture (%)
		default:	//option 10 or any other value
			cout << "For now in this prototype feature, we will make the specifications of this plant the "<< endl;
			cout << "same as a common houseplant" << endl;
			itemp[1] = 15;	//temp range
			itemp[2] = 30;
			ihum_req = 375;		//humidity (measured in ppm)
			imos_req = 0.15;	//moisture (%)
	}
	//display of living conditions for the plant
	cout << endl;
	cout << "Required Conditions for the Plant" << endl;
	cout << "_________________________________" << endl;
	cout << "Humidity = " << ihum_req << "ppm" << endl;
	cout << "Moisture = " << imos_req << "%" << endl;
	cout << "Temp. Range Required = " << itemp[1] << "oc - " << itemp[2] << "oc" << endl;
	cout << endl;
	cout << endl;
	for (icount = 1;icount <= 4; ++icount){	// we will be doing 4 runs for the purpose of this prototype
		//all values will be randomised
			//this is the simulation of the pant monitor actually collecting it's data
		ihum = 1 + rand() % 90;
		itemp[3] = 1 + rand() % 35;
		imos = 1 + rand() % 60;
		imos = imos/100;			//unit conversion (%)
		//display of the sensor values
		cout << "Humidity = " << ihum << "ppm"<< endl;
		cout << "Moisture = " << imos << "%"<< endl;
		cout << "Temp. Range Required = " << itemp[1] << "oc" << " - " << itemp[2] << "oc"<< endl;
		cout << "Current temperature = " << itemp[3] << "oc"<< endl;
		cout << endl;
		//sleep (5000);	//time delay of 5 seconds
		//this will be treated as the change of data every hour, therefore it will be eventually changed from 5 seconds to 1 hour
		//these if statements are for checking the largest value from the sensor values
		if (ihum>ihummax){
		    ihummax = ihum;
		}
		if (imos>imosmax){
		    imosmax = imos;
		}
		if (itemp[3]>itempmax){
		    itempmax = itemp[3];
		}	
	}
	cout << endl;
	//display of the highest values of all sensors
	cout << "Humidity high = " << ihummax <<"ppm" << endl;
	cout << "Moisture high = " << imosmax << "%" << endl;
	cout << "Current temperature high = " << itempmax << "oc" << endl;
	return 0;	
}
/*soon to add:
	-finding min value of all sensor values
	-finding averages of all sensor values
	-code to retrieve data from the sensor
	-more sufficient error trapping
	-warnings if the values from the fixed sensor values are out of range of the varying sensor value
	-having the name of the plant in the system
*/ 
