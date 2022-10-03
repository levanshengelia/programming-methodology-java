
ამოცანის პირობა:
მომხმარებელს შეყავს დადებითი რიცხვები, მანამ სანამ არ შეიყვანს -1 ს, დაბეჭდეთ რაოდენობა რამდენი ლუწი რიცხვი შეყვანა მომხმარებელმა.

ამ ამოცანის ამოსახსნელად საჭიროა მოვიფიქროთ თუ როგორ წავიკითხავთ რიცხვებს მომხმარებლისგან. ვინაიდან დამოკიდებულები ვართ იმაზე თუ როდის შემოვა მონაცემებში -1 და არ ვიცით ზუსტი რაოდენობა წასაკითხი რიცხვებისა, ამიტომ გამოვიყენოთ while. ამის გარდა საჭიროა ყოველი რიცხვი შევამოწმოთ და გავიგოთ ლუწია თუ არა.  

ამოხსნის გზა (1):
პირველ რიგში შევქმნათ int ტიპის ცვლადი, სადაც შევინახავთ ლუწი რიცხვების რაოდენობას. წავიკითხოთ რიცხვები while ციკლით მანამ სანამ არ შემოვა -1 (რომელიც კონსტანტად გვექნება აღწერილი) და შემოსვლისთანავე შევამოწმოთ მისი ლუწობა. თუ ლუწია შემოსული რიცხვი მაშინ გავზარდოთ ლუწი რიცხვების მთვლელი int ცვლადი. როდესაც მომხმარებელი შემოიყვანს -1-ს დავბეჭდოთ ზემოთხსენებული ცვლადი.

```java
	public static final int SENTINEL = -1;
	public void run() {
		int evens = 0;
		while(true) {
			int input = readInt("Enter a number: ");
			if(input == SENTINEL) {
				break;
			}
			if(input % 2 == 0) {
				evens++;
			}
		}
		println("The total number of even numbers are: " + evens);
	}
```

ამოხსნის გზა (2):
განსხვავებით პირველი მიდგომისგან , სადაც ერთდროულად ვკითხულობდით რიცხვს და თან ვამოწმებდით,  შეგვიძლია ამოცანა ორ სხვადასხვა პუნქტად დავყოთ: 1) წავიკითხოთ while-ით ყველა რიცხვი და შევინახოთ ისინი სიაში (ArrayList<Integer> ტიპის). 2) გადავუყვეთ სიას და დავითვალოთ მასში ლუწი რიცხვების რაოდენობა რაიმე int ტიპის მთვლელით.

```java
	public static final int SENTINEL = -1;
	public void run() {
		ArrayList<Integer> numbers = new ArrayList<>();
		while(true) {
			int input = readInt("Enter a number: ");
			if(input == SENTINEL) {
				break;
			}
			numbers.add(input);
		}
		int evens = 0;
		for(int i = 0; i < numbers.size(); i++) {
			if(numbers[i] % 2 == 0) {
				evens++;
			}
		}
		println("The total number of even numbers are: " + evens);
	}
```

მიუხედავად სისწორისა ეს მიდგომა შედარებით არაოპტიმალურია, ვინაიდან ვინახავთ ყველა რიცხვს როცა ამის საჭიროება არ არის. შეგვეძლო შემოსვლისთანავე შეგვემოწმებინა და უბრალოდ დაგვევიწყებინა ის რიცხვი, როგორც ეს ვქენით პირველ ამოხსნაში

*კოდის უნივერსალურობა:
ამოხსნა იმუშავებს ნებისმიერი შემოტანილი ინფორმაციისთვის (თუ შემოტანილი რიცხვები იქნება int-ის საზღვრებში), ვინაიდან კოდი არ არის დამოკიდებული რომელიმე კონკრეტული ცვლადის მნიშვნელობაზე გარდა. პირობაში ნახსენებია, რომ წაკითხვა -1-ის შემოსვლის შემდეგ უნდა დავასრულოთ და შეგვეძლო კოდში SENTINEL-ის მაგივრად -1 გამოგვეყენებინა. თუმცა უკეთესია ეს მნიშვნელობა კონსტანტად აღვწეროთ და კოდი ამ ცვლადზე დამოკიდებული გავხადოთ, რათა შემდგომში თუ მომხმარებელს მოუნდება, რომ მაგალითად -1-ის ნაცვლად 0-ზე შეწყდეს წაკითხვა, მხოლოდ ერთ ადგილას მოუწევს ამ ინფორმაციის ჩასწორება და კოდი სწორად იმშავებს. წინააღმდეგ შემთხვევაში მოუწევდა კოდში ყველა -1-ის 0-ად გადასწორება. ამ ყველაფერთან ერთად SENTINEL უფრო კითხვადია კოდის მნახველისთვის ვიდრე -1.

*შესაძლო შეცდომა:
შესაძლო შეცდომა შეიძლება იყოს -1-ის შემოსვლის შემდეგ მისი შემოწმება არის თუ არა ის ლუწი.

```java
	int input = 0;
	while(input != SENTINEL) {
		input = readInt();
		if(input % 2 == 0) {
			evens++;
		}
	}
```
ჩვენს შემთხვევაში, როცა SENTINEL არის -1, პასუხი მაინც სწორი დაგვიბრუნდება, ვინაიდან ის კენტია და ლუწი რიცხვების რაოდენობა არ გაიზრდება, თუმცა თუ მომხმარებელმა შეცვალა SENTINEL რაიმე ლუწი რიცხვით, მაშინ პროგრამა ერთით ზედმეტ პასუხს მოგვცემს და გამოდის, რომ პროგრამის სისწორე დამოკიდებული ხდება შემოტანილ მონაცემებზე, რაც ცუდია. ამასთან პროგრამა ერთით მეტ რიცხვს განიხილავ ვიდრე უნდა განიხილავდეს.