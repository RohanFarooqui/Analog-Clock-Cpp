#include <SFML\Graphics.hpp>
#include <SFML\Audio.hpp>
#include <cmath>
#include <ctime>
#include <iostream>
#include <windows.h>
#include <fstream>
#include <iomanip>
#include <cctype>
#include <sstream>

using namespace std;

float i=0;
bool check = false;
int AnalogClock();
int set_time();
int credits();
int minutetable();
int main()
{
    sf::RenderWindow window(sf::VideoMode(1024,768), "MENU ");
    sf::Vector2f windowCenter = sf::Vector2f(window.getSize().x / 2.0f, window.getSize().y / 2.0f);
    window.setMouseCursorVisible(false);
    sf::View fixed = window.getView();


    sf::Font font;
    font.loadFromFile("arial.ttf");

    sf::Text menu("MENU", font);
    menu.setCharacterSize(100);
    menu.setOrigin(140,350);
    menu.setPosition(window.getSize().x / 2 + 2, window.getSize().y / 2 + 2);
    menu.setStyle(sf::Text::Bold);
    menu.setColor(sf::Color::White);



    sf::Texture play1;
    if (!play1.loadFromFile("play.png")){return EXIT_FAILURE;}
    sf::Sprite play;
    play.setTexture(play1);
    play.setOrigin(390,180);
    play.setPosition(window.getSize().x / 2 + 2, window.getSize().y / 2 + 2);

    sf::Texture settime1;
    if (!settime1.loadFromFile("settime.png")){return EXIT_FAILURE;}
    sf::Sprite settime;
    settime.setTexture(settime1);
    settime.setOrigin(390,45);
    settime.setPosition(window.getSize().x / 2 + 2, window.getSize().y / 2 + 2);

    sf::Texture default1;
    if (!default1.loadFromFile("default.png")){return EXIT_FAILURE;}
    sf::Sprite default2;
    default2.setTexture(default1);
    default2.setOrigin(-200,180);
    default2.setPosition(window.getSize().x / 2 + 2, window.getSize().y / 2 + 2);

    sf::Texture nv;
    if (!nv.loadFromFile("needlevalue.png")){return EXIT_FAILURE;}
    sf::Sprite n;
    n.setTexture(nv);
    n.setOrigin(-200,50);
    n.setPosition(window.getSize().x / 2 + 2, window.getSize().y / 2 + 2);

    sf::Texture credit1;
    if (!credit1.loadFromFile("credit.png")){return EXIT_FAILURE;}
    sf::Sprite credit;
    credit.setTexture(credit1);
    credit.setOrigin(100,-20);
    credit.setPosition(window.getSize().x / 2 + 2, window.getSize().y / 2 + 2);

    sf::Texture exit1;
    if (!exit1.loadFromFile("exit.png")){return EXIT_FAILURE;}
    sf::Sprite exit2;
    exit2.setTexture(exit1);
    exit2.setOrigin(100,-100);
    exit2.setPosition(window.getSize().x / 2 + 2, window.getSize().y / 2 + 2);

    sf::Texture sfml;
    if (!sfml.loadFromFile("sfmllogo.png")){return EXIT_FAILURE;}
    sf::Sprite sfmll;
    sfmll.setTexture(sfml);
    sfmll.setOrigin(510,-260);
    sfmll.setPosition(window.getSize().x / 2 + 2, window.getSize().y / 2 + 2);

    sf::Text owner("M.ROHAN FAROOQUI ©", font);
    owner.setCharacterSize(30);
    owner.setOrigin(-150,-350);
    owner.setPosition(window.getSize().x / 2 + 2, window.getSize().y / 2 + 2);
    owner.setStyle(sf::Text::Bold);
    owner.setColor(sf::Color::Red);


    sf::Texture background;
    if (!background.loadFromFile("anonymous.png")){return EXIT_FAILURE;}
    sf::Sprite background1;
    background1.setTexture(background);

    sf::Texture texture;
    texture.loadFromFile("cursor.png");
    sf::Sprite sprite1(texture);



    while (window.isOpen()){
        sf::Event event;
        if (event.type == sf::Event::MouseButtonPressed){
        if (event.mouseButton.button == sf::Mouse::Left){
              if((event.mouseButton.x >=126 &&  event.mouseButton.x<=304 && event.mouseButton.y>=210 && event.mouseButton.y<=253 ))
                                          {window.close();
                                           AnalogClock();}
             if((event.mouseButton.x >=719 &&  event.mouseButton.x<=895 && event.mouseButton.y>=210 && event.mouseButton.y<=254 ))
                                          {ofstream out;
                                          out.open("Save.txt", std::ofstream::out | std::ofstream::trunc);
                                          out<<i;
                                          out.close();
                                          ofstream a;
                                          a.open("a.txt", std::ofstream::out | std::ofstream::trunc);
                                          a<<i;
                                          a.close();
                                          ofstream b;
                                          b.open("b.txt", std::ofstream::out | std::ofstream::trunc);
                                          b<<i;
                                          b.close();}
              if((event.mouseButton.x >=719 &&  event.mouseButton.x<=895 && event.mouseButton.y>=341 && event.mouseButton.y<=382 ))
                                          {
                                           window.close();
                                           minutetable();
                                          }
              if((event.mouseButton.x >=126 &&  event.mouseButton.x<=304 && event.mouseButton.y>=346 && event.mouseButton.y<=381 ))
                                          {window.close();
                                            set_time();}
              if((event.mouseButton.x >=416 &&  event.mouseButton.x<=596 && event.mouseButton.y>=410 && event.mouseButton.y<=456 ))
                                          {window.close();
                                          credits();}
              if((event.mouseButton.x >=416 &&  event.mouseButton.x<=596 && event.mouseButton.y>=491 && event.mouseButton.y<=534 ))
                                          {exit(0);}





}}
     while (window.pollEvent(event)){
            if (event.type == sf::Event::Closed)
                {window.close();}}
        window.draw(background1);
        window.draw(sfmll);
        window.draw(menu);
        window.draw(play);
        window.draw(default2);
        window.draw(n);
        window.draw(settime);
        window.draw(credit);
        window.draw(exit2);
        window.draw(owner);
        sprite1.setPosition(static_cast<sf::Vector2f>(sf::Mouse::getPosition(window)));
        window.setView(fixed);
        window.draw(sprite1);
        window.display();}


}


int AnalogClock()
{
    int x; int y;
    float sec;
    float min;
    float hour;
    float hourHandAngle;
    float minuteHandAngle;
    float secondHandAngle;
    float angle=0.0;
    float read;
    int clocksize = 250;// radius
    sf::RenderWindow window(sf::VideoMode(1024,768), "Analog Clock ");//clock wali window
    sf::Vector2f windowCenter = sf::Vector2f(window.getSize().x / 2.0f, window.getSize().y / 2.0f);//automatoc setting
    sf::CircleShape dot[60];// dot ki array 60

    //clock circle
    sf::CircleShape clockCircle(clocksize);
    clockCircle.setPointCount(100);
    clockCircle.setOutlineThickness(2);
    clockCircle.setOutlineColor(sf::Color::Black);
    clockCircle.setOrigin(clockCircle.getGlobalBounds().width / 2, clockCircle.getGlobalBounds().height / 2);
    clockCircle.setPosition(window.getSize().x / 2 + 2, window.getSize().y / 2 + 2);

    //center circle
    sf::CircleShape centercircle(10);
    centercircle.setPointCount(100);
    centercircle.setOutlineThickness(2);
    centercircle.setOutlineColor(sf::Color::Red);
    centercircle.setOrigin(11,15);
    centercircle.setFillColor(sf::Color::Red);
    centercircle.setPosition(window.getSize().x / 2 + 2, window.getSize().y / 2 + 2);

    //Second Hand Making
	sf::RectangleShape secondHand;
	secondHand.setSize (sf::Vector2f (1,210));
	secondHand.setOrigin(secondHand.getGlobalBounds().width/2,secondHand.getGlobalBounds().height-25);
	secondHand.setPosition(windowCenter);
	secondHand.setFillColor (sf::Color::Red);

	//Minute Hand Making
	sf::RectangleShape minuteHand;
	minuteHand.setSize (sf::Vector2f (3,210));
	minuteHand.setOrigin(minuteHand.getGlobalBounds().width/2,minuteHand.getGlobalBounds().height-25);
	minuteHand.setPosition(windowCenter);
	minuteHand.setFillColor (sf::Color::Black);

    //Hour Hand Making
	sf::RectangleShape hourHand;
    hourHand.setSize (sf::Vector2f (4,140));
    hourHand.setOrigin(hourHand.getGlobalBounds().width / 2, hourHand.getGlobalBounds().height - 25);
    hourHand.setPosition(windowCenter);
    hourHand.setFillColor (sf::Color::Black);

    //Back-Ground  outside the circle
    sf::Texture clockBrand;
    if (!clockBrand.loadFromFile("vv.jpg")){return EXIT_FAILURE;}
    sf::Sprite clockBrandSprite;
    clockBrandSprite.setTexture(clockBrand);

    //inside Image Clock
    sf::Texture clockinsideImage;
    if (!clockinsideImage.loadFromFile("clock.gif")){return EXIT_FAILURE;}
    clockCircle.setTexture(&clockinsideImage);



    //Dots in Circle
    for (int i=0; i<60; i++){
        x = (clocksize - 10) * cos(angle);
        y = (clocksize - 10) * sin(angle);
        if(i%5 == 0){dot[i]=sf::CircleShape(5);}
        else{dot[i] = sf::CircleShape(1);}
        dot[i].setFillColor(sf::Color::Black);
        dot[i].setOrigin(dot[i].getGlobalBounds().width / 2, dot[i].getGlobalBounds().height / 2);
        dot[i].setPosition(x + window.getSize().x / 2, y + window.getSize().y / 2);
        angle = angle + ((2 * 3.14)/60 );}
    //Button Load
    sf::Texture back1;
    if (!back1.loadFromFile("images.jpg")){return EXIT_FAILURE;}
    sf::Sprite back;
    back.setTexture(back1);
    back.setOrigin(513,385);
    back.setPosition(window.getSize().x / 2 + 2, window.getSize().y / 2 + 2);
    //Tic Tic Music
    sf::Music clockTick;
      if (!clockTick.openFromFile("tic.wav"))
        return EXIT_FAILURE;
        clockTick.setLoop(true);
        clockTick.play();

   //file Handling
   float z;
   float d;
   float a;
   float b;
   ifstream g;
   ifstream h;
   ofstream i;
   ifstream k;
   g.open("a.txt");
   g>>a;
   h.open("b.txt");
   h>>b;

   z=a+(b);
   i.open("Save.txt", std::ofstream::out | std::ofstream::trunc);
   i<<z;
   g.close();
   h.close();
   i.close();
   //Real File Handling
   k.open("Save.txt");
   k>>read;
   sec= read * 4315;

   while (window.isOpen()){
        sf::Event event;

        sf::Clock clock;

        sec=sec+1;
        secondHandAngle = (sec *6.0);
        secondHand.setRotation(secondHandAngle);
        minuteHandAngle = (sec / 12.0);
        minuteHand.setRotation(minuteHandAngle);
        hourHandAngle = (sec / 150.0);
        hourHand.setRotation(hourHandAngle);
        //cout<<hourHandAngle<<" "<<":"<<"   "<<minuteHandAngle<<"   "<<":"<<"     "<< secondHandAngle<<endl;


        if (event.type == sf::Event::MouseButtonReleased){
        if (event.mouseButton.button == sf::Mouse::Left){
              if((event.mouseButton.x >=0 &&  event.mouseButton.x<=201 && event.mouseButton.y>=0 && event.mouseButton.y<=73 ))
                                          {
                                             ofstream out;
                                             out.open("Save.txt", std::ofstream::out | std::ofstream::trunc);
                                             out<<sec;
                                             out.close();
                                             check = true;
                                             clockTick.stop();
                                             window.close();
                                              main();  }}}
        if(check==true){
           Sleep(0.0001);
           clock.restart();
           check = false;}
        else{
             clock.restart();
             Sleep(1000);}


    while (window.pollEvent(event)){
            if (event.type == sf::Event::Closed)
                window.close();}
                window.draw(clockBrandSprite);
                window.draw(clockCircle);
                window.draw (hourHand);
		        window.draw (minuteHand);
		        window.draw (secondHand);
		        window.draw(centercircle);
		        for (int i=0; i<60; i++){window.draw(dot[i]);}
                window.draw(back);
                window.display();}
}


int set_time()
{

    sf::RenderWindow window(sf::VideoMode(1024,768), "SET TIME");
    sf::Vector2f windowCenter = sf::Vector2f(window.getSize().x / 2.0f, window.getSize().y / 2.0f);


    sf::Font font;
    font.loadFromFile("arial.ttf");

    sf::Text hour("Enter Hours :", font);
    hour.setCharacterSize(40);
    hour.setOrigin(500,200);
    hour.setPosition(window.getSize().x / 2 + 2, window.getSize().y / 2 + 2);
    hour.setStyle(sf::Text::Bold);
    hour.setColor(sf::Color::Red);

    sf::Text minute("Enter Minutes :", font);
    minute.setCharacterSize(40);
    minute.setOrigin(500,100);
    minute.setPosition(window.getSize().x / 2 + 2, window.getSize().y / 2 + 2);
    minute.setStyle(sf::Text::Bold);
    minute.setColor(sf::Color::Red);

    sf::Texture clockBrand;
    if (!clockBrand.loadFromFile("anon.jpg")){return EXIT_FAILURE;}
    sf::Sprite clockBrandSprite;
    clockBrandSprite.setTexture(clockBrand);

    sf::Texture hour1;
    if (!hour1.loadFromFile("enterhours.png")){return EXIT_FAILURE;}
    sf::Sprite hours;
    hours.setTexture(hour1);
    hours.setOrigin(240,200);
    hours.setPosition(window.getSize().x / 2 + 2, window.getSize().y / 2 + 2);

    sf::Texture minute1;
    if (!minute1.loadFromFile("enterminutes.png")){return EXIT_FAILURE;}
    sf::Sprite minutes;
    minutes.setTexture(hour1);
    minutes.setOrigin(200,100);
    minutes.setPosition(window.getSize().x / 2 + 2, window.getSize().y / 2 + 2);


    sf::Text a("", font);
    a.setCharacterSize(20);
    a.setStyle(sf::Text::Bold);
    a.setPosition(280,200);
    a.setColor(sf::Color::Black);
    sf::String c;

    sf::Text b("",font);
    b.setCharacterSize(20);
    b.setStyle(sf::Text::Bold);
    b.setPosition(325,300);
    b.setColor(sf::Color::Black);
    sf::String d;

    sf::Texture ba;
    if (!ba.loadFromFile("images.jpg")){return EXIT_FAILURE;}
    sf::Sprite bac;
    bac.setTexture(ba);
    bac.setOrigin(513,385);
    bac.setPosition(window.getSize().x / 2 + 2, window.getSize().y / 2 + 2);


    float x;
    float y;
    float z;


    while (window.isOpen()){
    sf::Event event;
      if (event.type == sf::Event::MouseButtonReleased){
      if (event.mouseButton.button == sf::Mouse::Left){
      if((event.mouseButton.x >=0 &&  event.mouseButton.x<=201 && event.mouseButton.y>=0 && event.mouseButton.y<=73 )){
                window.close();
                main();
       }}}

    while (window.pollEvent(event)){
      if ((sf::Mouse::getPosition(window).x >= 275 && sf::Mouse::getPosition(window).x <= 532) &&(sf::Mouse::getPosition(window).y >= 186 && sf::Mouse::getPosition(window).y <= 240)){
      if (event.type == sf::Event::TextEntered){
         if (event.text.unicode >= 48 && event.text.unicode <= 57){
                c += (char)(event.text.unicode);
                a.setString(c);
                ofstream out;
                out.open("a.txt",std::ofstream::out | std::ofstream::trunc);
                out<<(char)(event.text.unicode)<<endl;
                ofstream u;
                u.open("b.txt", std::ofstream::out | std::ofstream::trunc );
                u<<".";
                u.close();}}}
      if ((sf::Mouse::getPosition(window).x >= 314 && sf::Mouse::getPosition(window).x <= 573) &&(sf::Mouse::getPosition(window).y >= 288 && sf::Mouse::getPosition(window).y <= 336)){
      if (event.type == sf::Event::TextEntered){
        if (event.text.unicode >= 48 && event.text.unicode <= 57){
                ofstream out;
                out.open("b.txt",ios::app);
                d += (char)(event.text.unicode);
                b.setString(d);
                out  << (char)(event.text.unicode);
                out.close();}}}

     if (event.type == sf::Event::Closed)
                window.close();}
                  window.draw(clockBrandSprite);
                  window.draw(hour);
                  window.draw(minute);
                  window.draw(hours);
                  window.draw(minutes);
                  window.draw(bac);
                  window.draw(a);
                  window.draw(b);
                  window.display();

                  }
}

int credits()
{
    sf::RenderWindow window(sf::VideoMode(1024,768), "Credits");
    sf::Vector2f windowCenter = sf::Vector2f(window.getSize().x / 2.0f, window.getSize().y / 2.0f);

    sf::Font font;
    font.loadFromFile("arial.ttf");

    sf::Text credit("Credits", font);
    credit.setCharacterSize(100);
    credit.setOrigin(175,350);
    credit.setPosition(window.getSize().x / 2 + 2, window.getSize().y / 2 + 2);
    credit.setStyle(sf::Text::Bold);
    credit.setColor(sf::Color::White);

    sf::Texture credits;
    if (!credits.loadFromFile("credits.png")){return EXIT_FAILURE;}
    sf::Sprite credit1;
    credit1.setTexture(credits);
    credit1.setOrigin(400,200);
    credit1.setPosition(window.getSize().x / 2 + 2, window.getSize().y / 2 + 2);

    sf::Texture left1;
    if (!left1.loadFromFile("images.jpg")){return EXIT_FAILURE;}
    sf::Sprite left;
    left.setTexture(left1);
    left.setOrigin(513,385);
    left.setPosition(window.getSize().x / 2 + 2, window.getSize().y / 2 + 2);



    while (window.isOpen()){
        sf::Event event;
        if (event.type == sf::Event::MouseButtonReleased){
        if (event.mouseButton.button == sf::Mouse::Left){
              if((event.mouseButton.x >=0 &&  event.mouseButton.x<=201 && event.mouseButton.y>=0 && event.mouseButton.y<=73 ))
                                          {
                                             window.close();
                                             main();  }}}





     while (window.pollEvent(event)){
            if (event.type == sf::Event::Closed)
                window.close();}



        window.draw(credit);
        window.draw(credit1);
        window.draw(left);
        window.display();

}

}

int minutetable()
{
   sf::RenderWindow window(sf::VideoMode(1024,768), "Minute Chart");
   sf::Vector2f windowCenter = sf::Vector2f(window.getSize().x / 2.0f, window.getSize().y / 2.0f);

   sf::Font font;
   font.loadFromFile("arial.ttf");

   sf::Text min("MINUTE NEEDLE VALUES", font);
   min.setCharacterSize(40);
   min.setOrigin(250,300);
   min.setPosition(window.getSize().x / 2 + 2, window.getSize().y / 2 + 2);
   min.setStyle(sf::Text::Bold);
   min.setColor(sf::Color::White);

   sf::Texture table;
   if (!table.loadFromFile("table.png")){return EXIT_FAILURE;}
   sf::Sprite table1;
   table1.setTexture(table);
   table1.setOrigin(335,200);
   table1.setPosition(window.getSize().x / 2 + 2, window.getSize().y / 2 + 2);

    sf::Texture back1;
    if (!back1.loadFromFile("images.jpg")){return EXIT_FAILURE;}
    sf::Sprite back;
    back.setTexture(back1);
    back.setOrigin(513,385);
    back.setPosition(window.getSize().x / 2 + 2, window.getSize().y / 2 + 2);



    while (window.isOpen()){
        sf::Event event;
        if (event.type == sf::Event::MouseButtonReleased){
        if (event.mouseButton.button == sf::Mouse::Left){
              if((event.mouseButton.x >=0 &&  event.mouseButton.x<=201 && event.mouseButton.y>=0 && event.mouseButton.y<=73 ))
                                          {
                                             window.close();
                                             main();  }}}





     while (window.pollEvent(event)){
            if (event.type == sf::Event::Closed)
                window.close();}
        window.draw(min);
        window.draw(table1);
        window.draw(back);
        window.display();

}



}






