program lab_9;
type
	film=record
		 naz:string[200];
		 rik:integer;
		 stud:string[200];
		 rez:string[100];
		 end;
     var
     kino: file of film;
     kinoD: file of film;  
     flag:boolean;
     f:film;
begin
   assign (kino,'kino.txt');//заповнення файлу
   rewrite (kino);
   flag:=false;
   writeln('заповніть будь ласка фільмотеку');
   writeln('для препинення введіть ####');
   repeat
   write('назва фільму- ');
   readln(f.naz);
      if  f.naz<>'####' then
         begin
         writeln ('рік виходу');
         readln(f.rik);
         writeln ('студія');
         readln(f.stud);
         writeln ('режесер');
         readln(f.rez);
         write (kino,f);
         end
         else flag:=true;
     until flag;
     close (kino);
     reset (kino);
     assign (kinoD,'kinoD.txt');//заповнення файлу
     rewrite (kinoD);
     while not eof(kino) do
           begin
           read (kino,f);//провіряємо умови, як фільм підходить пишемо його в файл kinoD 
           if f.stud='довженко' then// можеш спробувати одним оператором через and але мій компілятор так не схотів
              if f.rik>1985 then
                 if f.rik<1992 then write (kinoD,f)
           end;
           close (kinoD);
           reset (kinoD);
     while not eof(kinoD) do //виводимо данні
           begin
           read (kinoD,f);
           writeln(f.naz,'  ',f.rik,'  ',f.stud,'   ',f.rez);
           end;
               
readln;   
end.     
