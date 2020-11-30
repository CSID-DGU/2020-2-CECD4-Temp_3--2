# 2020-2-CECD4-Temp_3--2
#include "opencv2/opencv.hpp"
#include <iostream>
#include<stdlib.h>
#include <windows.h>
#include <direct.h>
#define D 300
#define foot_tracking_frame 15
using namespace cv;
using namespace std;

class worker
{	
private:
	int worker_index;
	int cloth_top[3]; 
	int cloth_under[3];
	int isCmeraOn;
	float body_proportions;
	Point foot_tracking[20];
//method
};

void print(int count, Mat UI);

int main() {
	worker worker_arr[1000];
	int worker_count = 0;
	int entranc[4] = { 340, 300 ,230,650 };
	Mat UI = imread("D:/capstone2/cap_ui.JPG");
	int frame_counting(0);
	Size size = Size(1279, 703);
	int check(0);

	int delay = D / 24;
	VideoCapture cap1("D:/capstone2/result/1번카메라.avi");
	//VideoCapture cap2("D:/capstone2/result/3번카메라.avi");
	VideoCapture cap3("D:/capstone2/result/3번카메라.avi");
	//VideoCapture cap4("D:/capstone2/result/3번카메라.avi");
	//HOGDescriptor hog;
	//hog.setSVMDetector(HOGDescriptor::getDefaultPeopleDetector());
	Mat frame1;
	Mat frame2 = imread("D:/capstone2/result/2번카메라.JPG");
	Mat frame3;
	Mat frame4 = imread("D:/capstone2/result/4번카메라.JPG");
	//int nSecont = 3600;
	//int nCount = 0;
	/*
	while (cap.read(frame))
	{
		imshow("시스템화면", frame);

		line(frame, Point(entranc[0], entranc[1]), Point(entranc[2], entranc[3]), Scalar(0, 0, 255), 3);
		//imshow("입출구", frame);
		int helmet_check = 0;
		
		//보행자 영역을 검출한다.
		Mat people = frame.clone();
		vector<Rect> dtected;//보행자 영역을 담고 있는 vector
		hog.detectMultiScale(people, dtected);
		for (int i = 0; i < dtected.size(); i++) {
			String person_num = "person" + to_string(i);
			Mat subImage = frame(dtected.at(i));


			//safty의 경우
			Mat safty = subImage.clone();
			inRange(safty, Scalar(200, 0, 200), Scalar(255, 50, 255), safty);
			//imshow("safty", safty);
			Scalar temp = mean(safty);
			//cout << temp[0]<<"  "<< dtected.size()<<endl;
			if (temp[0] != 0) {
				//imshow(person_num, subImage);
				Point2d center_worker(dtected.at(i).x + (dtected.at(i).width / 2), dtected.at(i).y + (dtected.at(i).height * 5 / 6));
				if ((center_worker.x) >= entranc[0]) {//입장전
					rectangle(frame, center_worker, Point2d(center_worker.x + 1, center_worker.y + 1), Scalar(255, 0, 0), 10);

				}
				else {//입장후
					rectangle(frame, center_worker, Point2d(center_worker.x + 1, center_worker.y + 1), Scalar(0, 255, 0), 10);

				}


			}

			//danger의 경우
			Mat dager = subImage.clone();
			inRange(dager, Scalar(50, 140, 2), Scalar(150, 255, 60), dager);
			imshow("frame", frame);
			//imshow("dager", dager);
			Scalar temp1 = mean(dager);
			if (temp1[0] != 0) {
				imshow(person_num, subImage);
				Point2d center_worker(dtected.at(i).x + (dtected.at(i).width / 2), dtected.at(i).y + (dtected.at(i).height * 5 / 6));
				if ((center_worker.x) >= entranc[0]) {//입장전
					rectangle(frame, center_worker, Point2d(center_worker.x + 1, center_worker.y + 1), Scalar(255, 0, 0), 10);

				}
				else {//입장후
					rectangle(frame, center_worker, Point2d(center_worker.x + 1, center_worker.y + 1), Scalar(0, 255, 0), 10);
					//리스트 출력
				}
			}
			
			


			//cout << nCount << endl;
			//리스트 출력
		if (0<nCount && nCount <= 210) {
			system("cls");
			cout << "시스템 상황" << endl;
			cout << "입장한 사람 : 0명" << endl;
			cout << "안전모 착용자 : 0명" << endl;
			cout << "미확인자 : 0명" << endl;
			cout << "안전모 미착용자 : 0명" << endl;
		}
		else if (210<nCount && nCount <= 240) {
			system("cls");
			cout << "시스템 상황" << endl;
			cout << "입장한 사람 : 1명" << endl;
			cout << "안전모 착용자 : 0명" << endl;
			cout << "미확인자 : 0명" << endl;
			cout << "안전모 미착용자 : 1명" << endl;
		}
		else if (240 < nCount && nCount <= 290) {
			system("cls");
			cout << "시스템 상황" << endl;
			cout << "입장한 사람 : 2명" << endl;
			cout << "안전모 착용자 : 1명" << endl;
			cout << "미확인자 : 0명" << endl;
			cout << "안전모 미착용자 : 1명" << endl;
		}
		else if (290 < nCount && nCount <= 330) {
			system("cls");
			cout << "시스템 상황" << endl;
			cout << "입장한 사람 : 2명" << endl;
			cout << "안전모 착용자 : 1명" << endl;
			cout << "미확인자 : 1명" << endl;
			cout << "안전모 미착용자 : 0명" << endl;
		}
		else if (330 < nCount && nCount <= 400) {
			system("cls");
			cout << "시스템 상황" << endl;
			cout << "입장한 사람 : 2명" << endl;
			cout << "안전모 착용자 : 0명" << endl;
			cout << "미확인자 : 2명" << endl;
			cout << "안전모 미착용자 : 0명" << endl;
		}
		else if (400 < nCount && nCount <= 430) {
			system("cls");
			cout << "시스템 상황" << endl;
			cout << "입장한 사람 : 3명" << endl;
			cout << "안전모 착용자 : 1명" << endl;
			cout << "미확인자 : 1명" << endl;
			cout << "안전모 미착용자 : 1명" << endl;
		}
		else if (430 < nCount && nCount <= 450) {
			system("cls");
			cout << "시스템 상황" << endl;
			cout << "입장한 사람 : 3명" << endl;
			cout << "안전모 착용자 : 1명" << endl;
			cout << "미확인자 : 2명" << endl;
			cout << "안전모 미착용자 : 0명" << endl;
		}
		else {
			system("cls");
			cout << "시스템 상황" << endl;
			cout << "입장한 사람 : 2명" << endl;
			cout << "안전모 착용자 : 0명" << endl;
			cout << "미확인자 : 2명" << endl;
			cout << "안전모 미착용자 : 0명" << endl;
		}


		nCount++;
		if (nCount % (nSecont * 24) == 0) {
			nCount = 0;
		}
			if (waitKey(10) == 27)
				break;
	}



	}
		return 0;
	*/
char a;
cin >> a;
	while (1)
	{	
		UI = imread("D:/capstone2/cap_ui.JPG");
		frame_counting++;
		//cout << frame_counting++ << endl;
		if (!cap1.read(frame1)) {
			break;
		}
		//if (!cap2.read(frame2)) {
		//	break;
		//}
		if (!cap3.read(frame3)) {
			break;
		}
		//if (!cap4.read(frame4)) {
		//	break;
		//}

		//입출구선
		line(frame1, Point(entranc[0], entranc[1]), Point(entranc[2], entranc[3]), Scalar(0, 0, 255), 3);
		flip(frame1, frame1,1);
		//1번 카메라 영역
		Point s1(200, 55), e1(733, 353);
		rectangle(UI,s1, e1,Scalar(0,0,0),-1);
		//2번 카메라 영역
		Point s2(200 + 533 + 5, 55), e2(733 + 533 + 10, 353);
		rectangle(UI, s2, e2, Scalar(0, 0, 0), -1);
		//3번 카메라 영역
		Point s3(200, 55 + 5 + (353 - 55)), e3(733, 353 + 5 + (353 - 55));
		rectangle(UI, s3, e3, Scalar(0, 0, 0), -1);
		//4번 카메라 영역
		Point s4(200 + 533 + 5, 55 + 5 + (353 - 55)), e4(733 + 533 + 10, 353 + 5 + (353 - 55));
		rectangle(UI, s4, e4, Scalar(0, 0, 0), -1);

		//시스템 내용
		Point system_plat_s1(7, 60), system_plat_e1(190, 353);
		rectangle(UI, system_plat_s1, system_plat_e1, Scalar(62, 62, 62), -1);

		//안내방송
		Point system_plat_s2(7, 382), system_plat_e2(190, 695);
		rectangle(UI, system_plat_s2, system_plat_e2, Scalar(62, 62, 62), -1);
		
		//1번 카메라
		Mat Frame1_Resize;
		resize(frame1, Frame1_Resize, cv::Size((e1.x-s1.x), (e1.y-s1.y)));
		//imshow("Frame1_Resize", Frame1_Resize);
		cv::Mat imageROI1(UI, cv::Rect(s1,e1));
		cv::Mat mask1(Frame1_Resize);
		Frame1_Resize.copyTo(imageROI1, mask1);
		putText(UI, "Camera_1(Exit)", Point(s1.x,s1.y+25), 3, 1, Scalar(255, 255, 255));

		//2번 카메라
		Mat Frame2_Resize;
		resize(frame2, Frame2_Resize, cv::Size((e2.x - s2.x), (e2.y - s2.y)));
		//imshow("Frame2_Resize", Frame2_Resize);
		cv::Mat imageROI2(UI, cv::Rect(s2, e2));
		cv::Mat mask2(Frame2_Resize);
		Frame2_Resize.copyTo(imageROI2, mask2);
		putText(UI, "Camera_2", Point(s2.x, s2.y + 25), 3, 1, Scalar(255, 255, 255));

		//3번 카메라
		Mat Frame3_Resize;
		resize(frame3, Frame3_Resize, cv::Size((e3.x - s3.x), (e3.y - s3.y)));
		//imshow("Frame3_Resize", Frame3_Resize);
		cv::Mat imageROI3(UI, cv::Rect(s3, e3));
		cv::Mat mask3(Frame3_Resize);
		Frame3_Resize.copyTo(imageROI3, mask3);
		putText(UI, "Camera_3", Point(s3.x, s3.y + 25), 3, 1, Scalar(255, 255, 255));

		//4번 카메라
		Mat Frame4_Resize;
		resize(frame4, Frame4_Resize, cv::Size((e4.x - s4.x), (e4.y - s4.y)));
		//imshow("Frame4_Resize", Frame4_Resize);
		cv::Mat imageROI4(UI, cv::Rect(s4, e4));
		cv::Mat mask4(Frame4_Resize);
		Frame4_Resize.copyTo(imageROI4, mask4);
		putText(UI, "Camera_4", Point(s4.x, s4.y + 25), 3, 1, Scalar(255, 255, 255));
		
		print(frame_counting,UI);


		imshow("최종ui", UI);
		
		if (waitKey(delay) == 27)break;
		
		
	}

}

void print(int count, Mat UI) {

}
