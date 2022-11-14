#Robot

## ამოცანის პირობა:
დახატეთ რობოტის სახე კანვასზე.

## ამოხსნა:
პირველი რიგში უნდა მოვიფიქროთ ამ ამოცანის კარგი დეკომპოზიცია. დეკომპოზიცია ძალიან გვეხმარება, განსაკუთრებით როცა საქმე გრაფიკულ პროგრამასთან გვაქვს, ვინაიდან დეკომპოზიციის გარეშე ხშირად მოგვიწევს ერთი და იმავე კოდის ბევრჯერ დაწერა. 
ამ ამოცანისთვის გამოვიყენოთ შემდეგი დეკომპოზიცია: დავხატოთ კისერი, სახე, თვალები და პირი.

მთავარი მეთოდი მიიღებს ამგვარ სახეს:

private void drawRobot() {
	drawNeck();
	drawFace();
	drawEyes();
	drawMouth();
}

მას შემდეგ, რაც ამოცანა დავყავით ქვეამოცანებად, ახლა ვიფიქროთ თითოეულის იმპლემენტაციაზე. 

### დავიწყოთ drawNeck() მეთოდით:

private void drawNeck() {
	GRect neck = new GRect(getWidth() / 2 - NECK_WIDTH / 2, getHeight() - NECK_HEIGHT, NECK_WIDTH, NECK_HEIGHT);
	neck.setFilled(true);
	neck.setFillColor(Color.LIGHT_GRAY);
	add(neck);
}

ამ მეთოდით კანვასზე დაიხატება მართკუთხედი. კისერი უნდა დავხატოთ კანვასზე ჰორიზონტალურად გათანაბრებულად, ანუ მარჯვენა და მარცხენა კანვასის კიდეებამდე დაშორება უნდა იყოს თანაბარი ნებისმიერი კანვასის ზომისათვის, ამიტომაც აუცილებელია, რომ მართკუთხედის მდებაორება დამოკიდებული გავხადოთ getWidth() ცვლადზე, რომელიც აღნიშნავს კანვასის სიგანეს. ასევე კოდის ადვილად შეცვლის შესაძლებლობის შესანარჩუნებლად კარგი იქნება თუ გამოვიყენებთ კონსტანტებს კისრის ზომებისთვის. ამ შემთხვევაში ეს კონსტანტებია NECK_WIDTH და NECK_HEIGHT, რომლებიც აღნიშნავენ კისრის სიგანესა და სიმაღლეს. GRect neck არის მართკუთხედის ობიექტი, რომელსაც გააჩნია ორნაირი კონსტრუქტორი (ანუ ორნაირად შეგვიძლია აღვწეროთ). პირველი ვარიანტი არის ის რაც წერია, ანუ გადავცეთ  სიგრძე/სიგანე/x/y და ასევე შეგვეძლო აღწერისას მხოლოდ სიგრძე/სიგანე გადაგვეცა, თუმცა ამ შემთხვევაში add-ში მოგვიწევდა კოორდინატების გადაცემა add(neck, x, y), ხოლო თუ არ გადავცემდით, დეფოლტად 0,0 კოორდინატებზე დახატავდა მართკუთხედს. neck.setFilled(true) - ეს ხაზი უზრუნველყოფს, რომ მართკუთხედის ობიექტს ჰქონდეს შიგთავსი. neck.setFillColor(Color.LIGHT_GRAY - ხოლო ეს ხაზი კი მართკუთხედის შიგთავსს აფერადებს იმ ფრად, რომელსაც გადავცემთ (ჩვენს შემთხვევაში LIGHT_GRAY). add არის ობიექტის კანვასზე გამოსაჩენი ბრძანება, მის გარეშე ობიექტი კანვასზე არ დაიხატება.

### drawFace() მეთოდი:

private void drawFace() {
	GRect face = new GRect(getWidth() / 2 - FACE_WIDTH / 2, getHeight() / 2 - FACE_LENGTH / 2, FACE_WIDTH,
			FACE_LENGTH);
	face.setFilled(true);
	face.setFillColor(Color.LIGHT_GRAY);
	add(face);
}

ამ მეთოდით კანვასზე დაიხატება რობოტის სახე. სახე, ისევე როგორც კისერი, ჰორიზონტალურად უნდა იყოს გათანაბრებული, ამიტომ მისი x კოორდინატიც getWidth() ცვლადზე დამოკიდებული უნდა იყოს. ასევე აქაც უნდა გამოვიყენოთ შესაბამისი კონსტანტები, გავაფერადოთ და საბოლოოდ დავამატოთ კანვასზე.

### drawEyes() მეთოდი:
private void drawEyes() {
	drawOneEye(getWidth() / 2 - FACE_WIDTH / 3);
	drawOneEye(getWidth() / 2 + FACE_WIDTH / 3 - EYE_SIZE);
}

ეს მეთოდი ხატავს ორ თვალს რობიტის სახეზე, რომლებიც უნდა იყოს რობოტის სახის ზომებსა და კანვასის სიგანეზე დამოკიდებული. აქ მნიშვნელოვანი დეტალია უნივერსალური მეთოდის გაკეთება. ვინაიდან ორივე თვალის დახატვა თითქმის ერთი და იგივე კოდის, ჩვენ შეგვიძლია ცალკე მეთოდი გავაკეთოთ და ორჯერ გამოვიძახოთ ნაცვლად იმისა, რომ ერთიდაიგივე კოდი ორჯერ დავწეროთ. ჯერ უნდა დავფიქრდეთ იმაზე თუ რა განასხვავებს თვალებს. თვალები ზუსტად ერთიდაიგივეა გარდა მათი მდებარეობისა. განსხვავებული აქვთ მხოლო x კოორდინატი. ამიტომაც შევქმანთ მეთოდი რომელსაც გადავცემთ x კოორდინატს, როგორც ცვლადს, და ეს მეთოდის დახატავს თვალს ამ x კოორდინატზე. ეს მეთოდი გამოიყურება ასე:

### drawOneEye(int x) მეთოდი:

private void drawOneEye(int x) {
	GRect eye = new GRect(width, getHeight() / 2 - FACE_LENGTH / 6, EYE_SIZE, EYE_SIZE);
	eye.setFilled(true);
	eye.setColor(Color.BLACK);
	add(eye);
}


### და ბოლოს drawMouth() მეთოდი:

private void drawMouth() {
	GRect mouth = new GRect(getWidth() / 2 - MOUTH_WIDTH / 2, getHeight() / 2 + MOUTH_OFFSET, 
			MOUTH_WIDTH, MOUTH_HEIGHT);
	mouth.setFilled(true);
	mouth.setColor(Color.BLACK);
	add(mouth);
}

ეს მეთოდი კანვასზე ხატავს რობოტის პირს, მართკუთხედს. ისევე როგორ ყველა სხვა ობიექტი ესეც, უნდა იყოს ჰორიზონტალურად შუაშია კანვაზე და ასევე რობოტის სახის შუაში, ამიტომაც აქაც საჭიროა ამ ცვლადებზე დამოკიდებული მართკუხედის ობიექტის შექმნა.

## შესაძლო ხარვეზები იმპლემენტაციისას:
1. კანვასის ზომების ცვლადების (getWidth() და getHeight()) გარეშე ობიექტების მდებარეობის განსაზღვრა, რაც გამოიწვევს იმას, რომ კოდის გამოვა ნაკლებად კითხვადი, მოგვიწევს ბევრი წვალება კოორდინატების ზუსტად შესარჩევად და სხვა ზომის კანვასზე რობოტის სახე არასწორად არ იქნება ისეთი პროპორცოული, როგორიც იყო თავდაპირველად.
2. დეკომპოზიციის გარეშე დაწერა. ამ შემთხვევაში მოგვიწევს მთლიანი კოდის ერთ მეთოდში დაწერა, რაც მას გახდის ძნელად წასაკითხსა და გასაგებს. ამასთან რთული იქნება კოდში შეცდომის პოვნა.