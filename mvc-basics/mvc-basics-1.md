## MVC Basics

> Useful [Video](https://www.youtube.com/watch?v=dTVVa2gfht8)

####Code used in the video:


###### MODEL
`CalculatorModel.java`

```java
// The Model performs all the calculations needed
// and that is it. It doesn't know the View
// exists

public class CalculatorModel {

	// Holds the value of the sum of the numbers
	// entered in the view

	private int calculationValue;

	public void addTwoNumbers(int firstNumber, int secondNumber){
		calculationValue = firstNumber + secondNumber;
	}

	public int getCalculationValue(){
		return calculationValue;
	}

}
```

###### VIEW

`CalculatorView.java`

```java
// This is the View
// Its only job is to display what the user sees
// It performs no calculations, but instead passes
// information entered by the user to whomever needs
// it.

import java.awt.event.ActionListener;

import javax.swing.*;

public class CalculatorView extends JFrame{

	private JTextField firstNumber  = new JTextField(10);
	private JLabel additionLabel = new JLabel("+");
	private JTextField secondNumber = new JTextField(10);
	private JButton calculateButton = new JButton("Calculate");
	private JTextField calcSolution = new JTextField(10);

	CalculatorView(){

		// Sets up the view and adds the components

		JPanel calcPanel = new JPanel();

		this.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
		this.setSize(600, 200);

		calcPanel.add(firstNumber);
		calcPanel.add(additionLabel);
		calcPanel.add(secondNumber);
		calcPanel.add(calculateButton);
		calcPanel.add(calcSolution);

		this.add(calcPanel);

		// End of setting up the components --------

	}

	public int getFirstNumber(){

		return Integer.parseInt(firstNumber.getText());

	}

	public int getSecondNumber(){

		return Integer.parseInt(secondNumber.getText());

	}

	public int getCalcSolution(){

		return Integer.parseInt(calcSolution.getText());

	}

	public void setCalcSolution(int solution){

		calcSolution.setText(Integer.toString(solution));

	}

	// If the calculateButton is clicked execute a method
	// in the Controller named actionPerformed

	void addCalculateListener(ActionListener listenForCalcButton){

		calculateButton.addActionListener(listenForCalcButton);

	}

	// Open a popup that contains the error message passed

	void displayErrorMessage(String errorMessage){

		JOptionPane.showMessageDialog(this, errorMessage);

	}

}
```

###### CONTROLLER
`CalculatorController.java`

```java
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;

// The Controller coordinates interactions
// between the View and Model

public class CalculatorController {

	private CalculatorView theView;
	private CalculatorModel theModel;

	public CalculatorController(CalculatorView theView, CalculatorModel theModel) {
		this.theView = theView;
		this.theModel = theModel;

		// Tell the View that when ever the calculate button
		// is clicked to execute the actionPerformed method
		// in the CalculateListener inner class

		this.theView.addCalculateListener(new CalculateListener());
	}

	class CalculateListener implements ActionListener{

		public void actionPerformed(ActionEvent e) {

			int firstNumber, secondNumber = 0;

			// Surround interactions with the view with
			// a try block in case numbers weren't
			// properly entered

			try{

				firstNumber = theView.getFirstNumber();
				secondNumber = theView.getSecondNumber();

				theModel.addTwoNumbers(firstNumber, secondNumber);

				theView.setCalcSolution(theModel.getCalculationValue());

			}

			catch(NumberFormatException ex){

				System.out.println(ex);

				theView.displayErrorMessage("You Need to Enter 2 Integers");

			}

		}

	}

}
```

###### PUTTING IT TOGETHER
`MVCCalculator.java`

```java
public class MVCCalculator {

    public static void main(String[] args) {

    	CalculatorView theView = new CalculatorView();

    	CalculatorModel theModel = new CalculatorModel();

        CalculatorController theController = new CalculatorController(theView,theModel);

        theView.setVisible(true);

    }
}
```