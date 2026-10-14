Felsökningsraport
Jaag arbetade med ett fel i bokningssystemet där det gick att boka ett mötesrum trots att rummet redan var bokat under samma tid.
Det var ett problem eftersom två kunder då kunde få samma rum saamtidigt.
Hur återskapade jag felet?
Jag utgick från exemplet där rummet Aspen redan var bokat mellan 09: 00 och 11:00 sedan undersökte jag vad som skuller 
hända om någon försökte boka samma rum mellan 08:00 och 10:00 eller mellan 10:00 och 12:00.
de tiderna överlappar den första bokninggen och ska därför inte godkännas.
Problemet i startprojektet var att vissa överlappande resultatet var att programet skulle stoppa den nya bokningen och visa ett felmedelande.
Däremot skaa en bokning mellan 11:00 och 12:00 var tillåten eftersom den första bokningen slutar precise när den andra börjar.
Jag undersökte valideringen i BookingService.cs. Problemt handlade om hur programet jämförde starttid och sluttid för två bokningar.
Om man bara kontrollerar vissa tider kan man missa att en ny bokning börjar före en befintlig bokning men ändå slutar mitt under den.Därför 
behövde kontrollen jämföra båda bokningen.
Jag ändrade kontrollen så att programmet undersöker om den nya bokningens starttid är tidigare än den befintliga bokningen sluttid är senare 
än den befintliga bokningens starttidd. Jag såg också till att kontrollen gäller samma rum och samma datum. Avbokade bokningar skaa inte
blockera nya vokningar. På det sättet kan prograammet upptäcka olika typer av överlappningar.Efter ädringen byggde jaag projektet i
Visual Studio och körde de automatiserde testerna.Resultatet blev att alla 14 tester gick igenom utan fel.
Create_WhenBookingOverlapsExis-tingBooking_ReturnsFailur kontrolleraar fyra olika överlappande tider och att de nekas.
Create_WhenBookingStartsWhenEX-istingBookingEnds_ReturnsSuc-cess kontrollerar att en bokning får börja direkt när den tidigare bokningen slutar.
Dessa tester hjälper att upptäcka om samma problem skulle komma tillbaka. Jag lärde mig att det är viktig att kontrollera hela tidsintervallen
och inte bara när en bokning börjar.