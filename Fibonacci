
package Fibonacci;

import java.awt.*;
import java.awt.event.*;
import java.io.*;
import java.util.ArrayList;
import javax.swing.*;


public class Fibonacci {
    public static class Graphic extends JFrame {
        
        //Creating the GUI 
        
        private JRadioButton iterative, recursive;
        private JLabel enterN, resultLabel, efficiencyLabel;
        private JTextField input, result, efficiency;
        private JButton compute;
        private ButtonGroup buttonGroup = new ButtonGroup();
        
        public Graphic() {
            setLayout(new GridBagLayout());
            GridBagConstraints window = new GridBagConstraints();
            
            window.insets = new Insets (1,1,1,1);
            
            iterative = new JRadioButton("Iterative");
            window.fill = GridBagConstraints.HORIZONTAL;
            window.gridx = 0;
            window.gridy = 0;
            add (iterative, window);
            buttonGroup.add(iterative);
            iterative.setSelected(true);
            
            recursive = new JRadioButton("Recursive");
            window.fill = GridBagConstraints.HORIZONTAL;
            window.gridx = 1;
            window.gridy = 0;
            add (recursive, window);
            buttonGroup.add(recursive);
            
            enterN = new JLabel("Enter n:");
            window.fill = GridBagConstraints.HORIZONTAL;
            window.gridx = 0;
            window.gridy = 1;
            window.gridwidth = 1;
            add (enterN, window);
            
            resultLabel = new JLabel("Result:");
            window.fill = GridBagConstraints.HORIZONTAL;
            window.gridx = 0;
            window.gridy = 3;
            window.gridwidth = 1;
            add (resultLabel, window);
            
            efficiencyLabel = new JLabel("Efficiency: ");
            window.fill = GridBagConstraints.HORIZONTAL;
            window.gridx = 0;
            window.gridy = 4;
            window.gridwidth = 1;
            add (efficiencyLabel, window);
            
            input = new JTextField(10);
            window.fill = GridBagConstraints.HORIZONTAL;
            window.gridx = 1;
            window.gridy = 1;
            window.gridwidth = 1;
            add (input, window);
            
            result = new JTextField(" ");
            window.fill = GridBagConstraints.HORIZONTAL;
            window.gridx = 1;
            window.gridy = 3;
            window.gridwidth = 1;
            add (result, window);
            
            efficiency = new JTextField(" ");
            window.fill = GridBagConstraints.HORIZONTAL;
            window.gridx = 1;
            window.gridy = 4;
            window.gridwidth = 1;
            add (efficiency, window);
            
            compute = new JButton("Compute");
            window.fill = GridBagConstraints.HORIZONTAL;
            window.gridx = 1;
            window.gridy = 2;
            window.gridwidth = 1;
            add (compute, window);
            
            //adding a listener for the compute button
            event mathAction = new event();
            compute.addActionListener(mathAction);
        }
        
        public static class Sequence {
            
            static private int efficiency = 1;
            static private int answer;
            
            //Compute Iterative uses a for loop and requires multiple variables in order to save the results from past runs of the loop
            public static int computeIterative (int n) {
                int last = 1;
                int secondLast = 0;
                if (n == 0 || n == 1) {
                    answer = n;
                    efficiency = n + 1;
                } else {
                    for (int i = 2; i <= n; i++) {
                        answer = (last * 2) + secondLast;
                        secondLast = last;
                        last = answer;
                        efficiency++;
                    }
                }
                return answer;
            }
            
            //Compute Recursive calls upon itself within the method, making it easier to write, and requiring few variables 
            //It's also much more versatile 
            public static int computeRecursive (int n) {
                if (n == 0 || n == 1) {
                    answer = n;
                    efficiency = n + 1;
                } else {
                    answer = (computeRecursive(n - 1) * 2) + computeRecursive(n - 2);
                    efficiency++;
                }
                return answer;
            }
            
            //method to get efficiency from either iterative or recursive runs
            public static int getEfficiency() {
                return efficiency;
            }   
        }
        
        public class event implements ActionListener {
            
            private int operand1;
            
            public void actionPerformed (ActionEvent mathAction) {
                
                String operators = mathAction.getActionCommand();
                Component frame = null;
               
                if (operators.equals("Compute")) {
                    try {
                        operand1 = Integer.parseInt(input.getText());
                        
                        //Loop that uses the sequence methods and displays the result/efficiency for either iterative or recursive
                        //then resets the efficiency to 1 for the next run
                        if (operand1 <= 15 && operand1 > 0) {
                            if(iterative.isSelected()) {
                                result.setText(String.valueOf(Sequence.computeIterative(operand1)));
                                efficiency.setText(String.valueOf(Sequence.getEfficiency()));
                            } else if (recursive.isSelected()) {
                                result.setText(String.valueOf(Sequence.computeRecursive(operand1)));
                                efficiency.setText(String.valueOf(Sequence.getEfficiency()));
                            }          
                            Sequence.efficiency = 1;
                        } else {    //input validation for numbers higher than 15 because at a certain point it starts to give incorrect answers or crash the program
                           JOptionPane.showMessageDialog(frame, "Please enter a whole number between 0 and 15", "Error Message", JOptionPane.ERROR_MESSAGE);
                        }
                    } catch (NumberFormatException e) { //input validation for non integer input
                        JOptionPane.showMessageDialog(frame, "Please Enter a whole number only", "Error Message", JOptionPane.ERROR_MESSAGE);
                    }
                }
            }
        }

        //Methods used to initiate and write to an array, then the array is written to an excel file
        public static class CreateFile {
            
            static ArrayList<String> dataLogArray = new ArrayList<>();
            
            //commas separate the data into separate boxes, and \n enters down to the next line
            public static void start () {
                dataLogArray.add("Method" + "," + "Input" + "," + "Output" + "," + "Efficiency" + "\n");
            }
            
            public static void writeValues (String method, int input, int output, int eff) {
                dataLogArray.add(method + "," + input + "," + output + "," + eff + "\n");
            }
            
            public static void finish() {
                try {
                    FileWriter dataLog = new FileWriter("Iterative and Recursive data.csv");
                    for (String str: dataLogArray) {
                        dataLog.append(str);
                    }
                    dataLog.close();
                } catch (IOException e) {
                    e.getMessage();
                }
            }
            
        }
        
        public static void main (String[] args) {
            //Code to actually create an instance of the GUI
            Graphic Box = new Graphic ();

            Box.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
            Box.setLocationRelativeTo(null);
            Box.setVisible(true);
            Box.setSize(350, 250);
            Box.setTitle("Iterative or Recursive");
            
            //Calling various methods in order to write the output values for n 0-10 to a .csv file
            CreateFile.start();
            for (int i = 0; i <= 10; i++) {
                int recursiveValue = Sequence.computeRecursive(i);
                int recursiveEfficiency = Sequence.getEfficiency();
                CreateFile.writeValues("Recursive", i, recursiveValue, recursiveEfficiency);
                Sequence.efficiency = 1;
            }
            for (int i = 0; i <= 10; i++) {
                int iterativeValue = Sequence.computeIterative(i);
                int iterativeEfficiency = Sequence.getEfficiency();
                CreateFile.writeValues("Iterative", i, iterativeValue, iterativeEfficiency);
                Sequence.efficiency = 1;
            }
            CreateFile.finish();
        }
    }   
}