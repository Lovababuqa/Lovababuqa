import 'cypress-xpath';
describe('FitPeo Revenue Calculator', () => {
    it('Adjusts the slider to 820', () => {
      // Step 1: Visit the FitPeo homepage
    //  cy.visit('https://www.fitpeo.com'); 
    cy.viewport(1280, 1024);
    cy.visit('https://www.fitpeo.com/revenue-calculator');
      // Step 2: Navigate to the Revenue Calculator page
  
      cy.contains('Revenue Calculator').click(); // Adjust this if needed for navigation
  
      // Step 3: Scroll down to the slider section
      cy.contains('h4', 'Medicare Eligible Patients')  
      .scrollIntoView()                            // Scroll to the element
      .then(() => {
        cy.log('Successfully scrolled to the "Medicare Eligible Patients" section');  // Success log
      });
  
      // Step 4: Adjust the slider to 820
    //  cy.get('input[data-index="0"]').invoke('val', 820).trigger('input')
    cy.xpath("//input[@type='number']")
      .clear() // Clear the input box before entering the value
      .type('820', { force: true }); // Type the entire number value
  
 // 2. Validate the position of the slider thumb
 cy.get('.MuiSlider-thumb:first') // Use :first to select the first thumb element
 .should('have.css', 'left') // Check the CSS 'left' property
 .and('match', /41%/); // Assert the thumb is at the correct position (820 / 2000 = 41%)

// If you need to ensure it matches the second thumb, you can target the second one explicitly
cy.get('.MuiSlider-thumb:last') // Use :last to select the second thumb element (if applicable)
 .should('have.css', 'left') // Check the CSS 'left' property
 .and('match', /41%/); // Assert the thumb is at the correct position (820 / 2000 = 41%)
 
  
      // Step 5: Verify that the text field value updates to 820
   //   cy.get('.revenue-calculator-textfield') // Replace with the actual selector for the text field
    //    .should('have.value', '820');
    cy.xpath("//input[@type='number']")
    .invoke('val') // Retrieve the current value of the input field
    .then((inputValue) => {
      // Log the value to the console
      cy.log('Input value:', inputValue);
      
      // Optionally, assert that the value is as expected (if needed)
      expect(inputValue).to.equal('820'); // Replace with the expected value
    });

    cy.xpath("(//input[@type='checkbox'])[1]").check();
      cy.xpath("(//input[@type='checkbox'])[2]").check();
      cy.xpath("(//input[@type='checkbox'])[3]").check();

      cy.xpath("//p[.='Total Recurring Reimbursement for all Patients Per Month']/following::p[1]")
      .invoke('text') // Get the text of the next <p> element
      .then((textValue) => {
        // Log the extracted text value to the console (optional)
        cy.log('Extracted value:', textValue);
        expect(textValue.trim()).to.equal('$98400');

   

      

   
  });
});
});
