# PRODIGY_SD_01
import javax.swing.*;
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;

public class TemperatureConverter extends JFrame {
    private JTextField inputField;
    private JComboBox<String> unitSelector;
    private JLabel resultLabel;

    public TemperatureConverter() {
        setTitle("SDE Task-01: Temperature Converter");
        setSize(400, 250);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setLayout(new GridLayout(4, 1, 10, 10));

        inputField = new JTextField();
        String[] units = {"Celsius", "Fahrenheit", "Kelvin"};
        unitSelector = new JComboBox<>(units);
        JButton convertButton = new JButton("Convert");
        resultLabel = new JLabel("Enter value and press Convert", SwingConstants.CENTER);

        add(new JLabel("Enter Temperature:", SwingConstants.CENTER));
        add(inputField);
        add(unitSelector);
        add(convertButton);
        add(resultLabel);

        convertButton.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                try {
                    double val = Double.parseDouble(inputField.getText());
                    String unit = (String) unitSelector.getSelectedItem();
                    convertAndDisplay(val, unit);
                } catch (NumberFormatException ex) {
                    resultLabel.setText("Error: Please enter a valid number");
                }
            }
        });
    }

    private void convertAndDisplay(double val, String unit) {
        double c, f, k;
        if (unit.equals("Celsius")) {
            c = val;
            f = (c * 9/5) + 32;
            k = c + 273.15;
        } else if (unit.equals("Fahrenheit")) {
            f = val;
            c = (f - 32) * 5/9;
            k = c + 273.15;
        } else {
            k = val;
            c = k - 273.15;
            f = (c * 9/5) + 32;
        }
        resultLabel.setText(String.format("C: %.2f | F: %.2f | K: %.2f", c, f, k));
    }

    public static void main(String[] args) {
        SwingUtilities.invokeLater(() -> new TemperatureConverter().setVisible(true));
    }
}
