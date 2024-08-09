import javax.swing.*;
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;

public class PercentageCalculator extends JFrame implements ActionListener {

    // Components of the GUI
    private JTextField input1Field, input2Field, resultField;
    private JButton calculateButton;
    private JComboBox<String> calculationType;

    public PercentageCalculator() {
        // Setting up the frame
        setTitle("Percentage Calculator");
        setSize(400, 300);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setLayout(new GridLayout(5, 2));

        // Labels
        add(new JLabel("Input 1:"));
        input1Field = new JTextField();
        add(input1Field);

        add(new JLabel("Input 2:"));
        input2Field = new JTextField();
        add(input2Field);

        add(new JLabel("Calculation Type:"));
        calculationType = new JComboBox<>(new String[]{"Percentage", "Percentage Increase", "Percentage Decrease", "Find Whole"});
        add(calculationType);

        calculateButton = new JButton("Calculate");
        calculateButton.addActionListener(this);
        add(calculateButton);

        add(new JLabel("Result:"));
        resultField = new JTextField();
        resultField.setEditable(false);
        add(resultField);

        setVisible(true);
    }

    @Override
    public void actionPerformed(ActionEvent e) {
        try {
            double input1 = Double.parseDouble(input1Field.getText());
            double input2 = Double.parseDouble(input2Field.getText());
            double result = 0;

            String selectedType = (String) calculationType.getSelectedItem();
            if ("Percentage".equals(selectedType)) {
                result = (input1 / input2) * 100;
            } else if ("Percentage Increase".equals(selectedType)) {
                result = ((input2 - input1) / input1) * 100;
            } else if ("Percentage Decrease".equals(selectedType)) {
                result = ((input1 - input2) / input1) * 100;
            } else if ("Find Whole".equals(selectedType)) {
                result = (input1 / input2) * 100;
            }

            resultField.setText(String.format("%.2f", result) + "%");

        } catch (NumberFormatException ex) {
            JOptionPane.showMessageDialog(this, "Invalid input. Please enter numeric values.", "Error", JOptionPane.ERROR_MESSAGE);
        }
    }

    public static void main(String[] args) {
        new PercentageCalculator();
    }
}
