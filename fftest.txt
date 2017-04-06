#include <stdio.h>
//Display yields before pieces lost prior to program
//Changes for heavier density
//Formula for feedrate
//Formula for pauses
//Tweak formula for b
//Tweak formulat for xm


int tph, tpw, yield, y2, sub, n, fy1, fy2, z;
float a, b, c, aa, bb, cc, xm;


void getDims() //Gets and alters dimensions
{
      printf("\n ____________                                   ____________");
      printf("\n \\__________/      8' FLUTE FILLER PROGRAM      \\__________/ \n\n");
      printf("When entering dimensions, be sure to enter all decimals. (ie, .0625, not .063)\n\n");
      printf("Enter the thickness:");
      scanf("%f", &aa);
      printf("Enter the top dimension:");
      scanf("%f", &bb);
      printf("Enter the bottom dimension:");
      scanf("%f", &cc);
      
      
      
      //if((bb-cc)/2 < aa) {b=bb+.0625;}
      //if((bb-cc)/2 == aa) {b=bb+.125;} //change, should be around .48?
      //if((bb-cc)/2 > aa) {b=bb+.1875;}
      b=bb+.25;
      
      //a=aa + .0625;
      a=aa;
      c=cc;
      
      return;
}



void detYield() //Calculates yields for both bun positions
{
 float pchf;
 int pch, pcw;    

    pcw=0;
    for(z=1; ((b-c)/2)+(z*(c+((b-c)/2))) <= 48; z++)
    {
     pcw++;
    }
    pchf= 36/a;
    
    pch=0; //turns pchf into an integer
       for(z=1; z<=pchf; z++)
       {
         pch++;
         }
    
    sub= pcw/2 * (1+pch/20);
    fy1= (pcw * pch) - (pcw/2);
    yield= pcw * pch - sub;
    //printf("pcw is %i\n", pcw);
    //printf("pch is %i\n", pch);
    //printf("sub is %i\n", sub);
    //printf("Yield is %i\n", yield);
    tpw=pcw;
    tph=pch;
    
    pcw=0;
    for(z=1; ((b-c)/2)+(z*(c+((b-c)/2))) <= 36; z++)
    {
     pcw++;
    }
    pchf= 48/a;
    
    pch=0; //turns pchf into an integer
       for(z=1; z<=pchf; z++)
       {
         pch++;
         }
    
    sub= pcw/2 * (1+pch/20);
    fy2= (pcw * pch) - (pcw/2);
    y2= pcw * pch - sub;
    //printf("pcw is %i\n", pcw);
    //printf("pch is %i\n", pch);
    //printf("sub is %i\n", sub);
    //printf("y2 is %i\n", y2);
    
    if(yield < y2)
    {
    yield=y2;
    tpw=pcw;
    tph=pch;
    }
    
    return;
}




void move1()
{
 
 printf("N%i G01 X%.4f\n", n, c + (xm + .25)); n=n+10;
 printf("N%i G04P1\n", n); n=n+10;
 printf("N%i G01 X-%.4f\n", n, (xm + .25)); n=n+10;
 printf("N%i G01 X%.4f Y%.4f\n", n, xm, a); n=n+10;
 printf("N%i G04P1\n", n); n=n+10;
 
 return;
}




void move2()
{
 printf("N%i G01 X%.4f\n", n, c + (xm + .25)); n=n+10;
 printf("N%i G04P1\n", n); n=n+10;
 printf("N%i G01 X-%.4f\n", n, xm + .25); n=n+10;
 printf("N%i G01 X%.4f Y-%.4f\n", n, xm, a); n=n+10;
 printf("N%i G04P1\n", n); n=n+10;
 
 return;
}
 

void dofrac()
{
int fa, z;

fa=0;
       for(z=1; z<=(aa * 16); z++)//turns aa into an integer (fa)
       {
         fa++;
       }
    if(fa % 16 == 0) {printf("%i ", fa/16);}
    if(fa % 16 == 1) {if (fa < 16){printf("1/16 ");} else {printf("%i 1/16 ", fa/16);}}
    if(fa % 16 == 2) {if (fa < 16){printf("1/8 ");} else {printf("%i 1/8 ", fa/16);}}
    if(fa % 16 == 3) {if (fa < 16){printf("3/16 ");} else {printf("%i 3/16 ", fa/16);}}
    if(fa % 16 == 4) {if (fa < 16){printf("1/4 ");} else {printf("%i 1/4 ", fa/16);}}
    if(fa % 16 == 5) {if (fa < 16){printf("5/16 ");} else {printf("%i 5/16 ", fa/16);}}
    if(fa % 16 == 6) {if (fa < 16){printf("3/8 ");} else {printf("%i 3/8 ", fa/16);}}
    if(fa % 16 == 7) {if (fa < 16){printf("7/16 ");} else {printf("%i 7/16 ", fa/16);}}
    if(fa % 16 == 8) {if (fa < 16){printf("1/2 ");} else {printf("%i 1/2 ", fa/16);}}
    if(fa % 16 == 9) {if (fa < 16){printf("9/16 ");} else {printf("%i 9/16 ", fa/16);}}
    if(fa % 16 == 10) {if (fa < 16){printf("5/8 ");} else {printf("%i 5/8 ", fa/16);}}
    if(fa % 16 == 11) {if (fa < 16){printf("11/16 ");} else {printf("%i 11/16 ", fa/16);}}
    if(fa % 16 == 12) {if (fa < 16){printf("3/4 ");} else {printf("%i 3/4 ", fa/16);}}
    if(fa % 16 == 13) {if (fa < 16){printf("13/16 ");} else {printf("%i 13/16 ", fa/16);}}
    if(fa % 16 == 14) {if (fa < 16){printf("7/8 ");} else {printf("%i 7/8 ", fa/16);}}
    if(fa % 16 == 15) {if (fa < 16){printf("15/16 ");} else {printf("%i 15/16 ", fa/16);}}
    
    return ;
}





main()
{
int nwires, pcount;
float xout;
n=100;


      getDims(); //Gets dimensions of piece from user
      if(cc > bb){printf("\n\nYou must enter the LARGER dimension as the top dimension.\n\n");getchar();getchar();return 0;}
      if(aa > 48){printf("\n\nPieces cannot be thicker than 48 inches!\n\n");getchar();getchar();return 0;}
      detYield(); //Determines bun position and yield
      xm = (b-c)/2;
      
	  nwires = tph + 1;
      //if (nwires > 20) {nwires = 20;}
      
      if (tph > 20) {nwires = ((tph/2)+ 1);}
	  if (tph > 20 && (tph % 2)) {nwires = nwires + 1;}
     
     
      
      
    //printf("\n\nTrim bun to 96IN\n");
    
    printf("\nYield for 36H x 48W if done in 1 pass: %i\n", fy1);
    printf("Yield for 48H x 36W if done in 1 pass: %i\n\n", fy2);
    
    printf("Adjust feedrate according to bun density and wetness.\n\n");
    printf("Adjust X move on diagonal moves to properly account for burnaway.\n\n");
    //printf("\n\nSet %i wires at %.4fIN\n", nwires, a);
    //if(tph > 20 && tph < 60) {printf("2 passes\n");}
    //if(tph >=60) {printf("(3 passes)\n");}
    //if(yield > y2) {printf("Bun position is 36H x 48W\n");}
    //else {printf("Bun position is 48H x 36W\n");}
    //printf("Yield is %i pcs. per bun\n\n\n", yield);
        
    
    //printf("a is %f\n", a);
    //printf("b is %f\n", b);
    //printf("c is %f\n", c);
    //printf("tpw is %i\n", tpw);
    //printf("tph is %i\n", tph);
    //printf("nwires is %i\n", nwires);
    //printf("pcw is %i\n", pcw);
    //printf("pch is %i\n", pch);
    //printf("pcx is %i\n", pcx);
    //printf("pcy is %i\n", pcy);
    //printf("sub is %i\n", sub);
    //printf("yield is %i\n", yield);
    
    
    printf("__________PROGRAM__________\n\n");
    printf("(");
    dofrac();
    printf("x ");
    aa=cc;
    dofrac();
    printf("- ");
    aa=bb;
    dofrac();
    printf("x 96 FLUTE FILLERS)\n");
    
    
    printf("(TRIM BUN TO 96IN)\n");
    printf("(SET %i WIRES @ %.4fIN)\n", nwires, a);
    
    if(tph > 20 && tph < 60) {printf("(2 PASSES)\n");}
    if(tph >=60) {printf("(3 PASSES)\n");}
    if(yield > y2) {printf("(BUN POSITION: 36H x 48W)\n");}
    else {printf("(BUN POSITION: 48H x 36W)\n");}
    
    printf("(YIELD IS %i PCS/BUN)\n\n", yield);
    printf("N10 G91\n");
    printf("N20 M34\n");
    printf("N30 G04P3\n");
    printf("N40 G01 X1 F18\n");
    printf("N50 G01 X%.4f\n", (xm + .25));
    printf("N60 G04P1\n");
    printf("N70 G01 X-%.4f\n", (xm + .25));
    printf("N80 G01 X%.4f Y-%.4f\n", xm, a);
    printf("N90 G04P1\n");
          
    pcount=0;
    while(pcount < tpw)
    {
       move1();
       pcount++;
       if(pcount < tpw)
       {
          move2();
          pcount++;
       }
    }
    
    if(yield > y2) {xout=54 - (xm + (tpw * (c + xm)));}
    else {xout=42 - (xm + (tpw * (c + xm)));}
               
    printf("N%i G01 X%.4f\n", n, xout); n=n+10;
    printf("N%i M35 M02\n\n", n);
    
    printf("__________________________________________________________\n");
    printf("To use this for your program:\n\n");
    
    printf("1. Right click the C:\\ in the upper left and choose EDIT then SELECT ALL.\n");
    printf("2. Repeat and select COPY.\n");
    printf("3. Paste to a new text document and edit as necessary.\n");
    printf("4. Be sure to remove all lines that are not program comments or code.\n");
    printf("5. Save as .JOB file.\n");
    printf("(Note - You may have to re-copy from NOTEPAD if you open AS3000.)");
    
    getchar();
    getchar();
    return 0 ;
}      

