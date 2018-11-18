# valuelist

public class ValueList {
	
	private static final String HEAD = "Head";
	private static final String TAIL = "null";
	private Values head;
	
	
	//Methode überprüft ob die Summe der aufeinander folgendenden Integer-Werte des Knotens > 25 sind.
	//Wenn ja, dann setze den Knoten auf TRUE
	public void appendList(){
		Values node = head;
		
		while(node != null && node.getNext() != null){
			int sum = node.getValue() + node.getNext().getValue();
			if(sum > 25){
				node.mark();
				node.getNext().mark();
				node = node.getNext();
			}else{
				node = node.getNext();
			}
		}
	}
	
	//Methode, die alle Knoten mit dem Wert TRUE aus der Liste entfernt
	public void clean(){
	}
	
	public static void main(String[] args){
		ValueList list1 = new ValueList();
		
		Values value1 = new Values("Value-1",7,false);
		Values value2 = new Values("Value-2",20, false);
		Values value3 = new Values("Value-3",13, false);
		Values value4 = new Values("Value-4",10, false);
		Values value5 = new Values("Value-5",8, false);
		
		list1.appendValues(value1);
		list1.appendValues(value2);
		list1.appendValues(value3);
		list1.appendValues(value4);
		list1.appendValues(value5);
		
		System.out.print("ValueList erstellt: \t\t");
		System.out.println(list1.toString());
		
		list1.appendList();
		
		System.out.print("ValueList nach Bearbeitung: \t");
		System.out.println(list1.toString());
		
		System.out.println("ValueList sollte so aussehen: \tHead--> Value-1(7, true)--> Value-2(20, true)--> Value-3(13, true)--> Value-4(10, false)--> Value-5(8, false)--> null");
		
		System.out.println("---------------------------------------------------------------------------------------------------------------------------------------------------------------------");
		System.out.println();
		
		
		ValueList list2 = new ValueList();
		
		Values value6 = new Values("Value-1",7,false);
		Values value7 = new Values("Value-2",20, false);
		Values value8 = new Values("Value-3",13, true);
		Values value9 = new Values("Value-4",10, true);
		Values value10 = new Values("Value-5",8, false);
		
		list2.appendValues(value6);
		list2.appendValues(value7);
		list2.appendValues(value8);
		list2.appendValues(value9);
		list2.appendValues(value10);
		
		System.out.print("ValueList erstellt: \t\t");
		System.out.println(list2.toString());
		
		list2.clean();
		
		System.out.print("ValueList nach Bearbeitung: \t");
		System.out.println(list2.toString());
		
		System.out.println("ValueList sollte so aussehen: \tHead--> Value-1(7, false)--> Value-2(20, false)--> Value-5(8, false)--> null");
		
		System.out.println("---------------------------------------------------------------------------------------------------------------------------------------------------------------------");
		System.out.println();
	}
	
	public int getSize(){
		int size = 0;		
		Values node = head;
		
		while(node != null){
			size++;
			node = node.getNext();
		}
		return size;
	}
	
	public void appendValues(Values value){	
		if(getSize() == 0){
			head = value;
		}else{
			Values node = head;
			int size = getSize();
			
			for(int i = 1; i < size; i++){
				node = node.getNext();
			}
			node.setNext(value);
		}
	}
	
	@Override
	public String toString() {
		if (getSize() == 0) {
			return HEAD;
		}

		StringBuilder str = new StringBuilder(HEAD);

		Values value = head;
		while (value != null) {
			str.append("-->");
			str.append(String.format(" %s(%d, %b)", value.getName(),
										value.getValue(),
										value.isMarked()));
			value = value.getNext();
		}

		return str.toString() + "--> " + TAIL;
		
	}
}


public class Values {

	private Values next;
	
	private boolean mark;
	private int value;
	private final String name;
	
	public Values(String name, int value, boolean mark){
		this.name = name;
		this.value = value;
		this.mark = mark;
	}
	
	public String getName(){
		return name;
	}
	
	public Values getNext(){
		return next;
	}
	
	public void setNext(Values next){
		this.next = next;
	}
	
	public int getValue(){
		return value;
	}
	
	public void setValue(int value){
		this.value = value;
	}
	
	public void mark(){
		mark = true;
	}
	
	public void unmark(){
		mark = false;
	}
	
	public boolean isMarked(){
		return mark;
	}
	
	@Override
	public String toString() {
		return name;
	}

}
