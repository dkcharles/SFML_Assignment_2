# SFML_Assignment_2
Assignment 2 Samples
/*
* An SFML application using a vector list to store point data - Darryl Charles
* SFML Documentation https://www.sfml-dev.org/documentation/2.5.1/
* Set up your own VS2019 project https://www.youtube.com/watch?v=lFzpkvrscs4
*
* ================= Group Streamers =================
*  Emmet Bloomer
* 
* 
* ADD MORE LATER
* ===================================================
*/

#include <iostream>                                                     
#include <SFML/Graphics.hpp> 
#include "time.h"
using namespace sf;

const int M = 20;
const int N = 10;

int field[M][N] = { 0 };

struct point
{int x, y;} a[4], b[4];

int figures[7][4] = //shapes // Double Check Line
{
	1,3,5,7 // I
	2,4,5,7 // Z
	3,5,4,6 // S
	3,5,4,6 // T
	2,3,4,5 // L 
	3,5,7,6 // J
	2,3,4,5 // O
};

bool
{ // Double Check Line
	for (int i = 0; i < 4; i++)
		if (a[i].x < 0 || a[i].y >= M) return 0;
		else if (field[a[i].y][a[i].x]) return 0;
	
return 1; 
	
};

int main()
{
	srand(time(0));
	RenderWindow window(VideoMode(320, 480), "The Game!");


	//Adds Picture Image//
	Texture t;
	t.loadFromFile("images/tiles.png");

	Sprite s(t);
	s.setTextureRect(IntRect(0, 0, 18, 18));

	int dx = 0; bool rotate = 0; int colorNum = 1;
		float timer = 0, delay = 0.3;

	Clock clock;

	while (window.isOpen())
	{
		float time = clock.getElapsedTime(); // Double Check Line
		clock.restart();
		timer += time;

		Event e;
		while (window.pollEvent(e))
		{
			if (e.type == Event::Closed)
				window.close();

			if (e.type == Event::KeyPressed)
				if (e.key.code == Keyboard::Up) rotate = true;
				if (e.key.code == Keyboard::Left) dx=-1;
				if (e.key.code == Keyboard::Right) dx=1;
		}

		if(Keyboard::isKeyPressed(Keyboard::Down)) delay=0.05


		//Move//
			for (int i = 0; i < 4; i++) { b[i] = a[i] }; {a[i].x += dx};   // Double Check Line
		if (!check()) for (int i = 0; i < 4; i++) a[i] = b[i];


		//Rotate//
		if (rotate)
		{
			Point p = a[1]; // enter of rotation // Double Check Line
			for (int i=0 ;i<4;i++)
			{
				int x = a[i].y - p.y;
				int y = a[i].x - p.x;
				a[i].x = p.x - x;
				a[i].y = p.y + y;

			}
			if (!check()) for (int i < 4; i++) a[i] = b[i]; // Double Check Line
		}

		//Tick//
		if (timer > delay)
		{
			for (int i = 0; i < 4; i++) a[i].y += 1;
			if (!check())
			{
				for (int i = 0; i < 4; i++) field[b[i].y][b[i].x] = colorNum;

				colorNum = 1 + rand() % 7;
				int n = rand() % 7;
				for(int i=0;i<4;i++)
				{
					a[i].x = figures[n][i] % 2
					a[i].y = figures[n][i] / 2 // Double Check Line
				}
			}
			timer = 0;
		}

		dx = 0; rotate = 0; delay = 0.3;


		//Check Lines//
		int k = M - 1;
		for (int i = M - 1; i > 0; 1--) // Double Check Line
		{
			int count = 0;
			for (int j = 0; j < N; j++)
			{
				if(field[i][j]) count++;
				field[k][k] = field[i][j];
			}
			if (count < N) k--;
		}


		//Draw//
		window.clear(Color::White);
		
		for(int i=0;i<M;i++)
			for (int i = 0; i < N; i++)
			{
				if (field[i][j] == 0) continue;
				s.setTextureRect(IntRect(field[i][j] * 18, 0, 18, 18));
				s.setPosition(j * 18, i * 18);
				window.draw(s);
		}
		for (int i = 0; i < 4; i++)
		{
			s.setTextureRect(IntRect(colorNum * 18, 0, 18, 18));
			s.setPosition(a[i].x*18,a[i].y*18);
			window.draw(s);
		}
		window.display();
	}

	return 0;
}
