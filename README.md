keyboard-offset
===============

as title, when keyboard appeared, let view be offsetted.


in @interface yourViewController : UIViewController <UITextFieldDelegate>

  BOOL bIsRaised;
  CGFloat cgfKeyboardHeight;
  CGFloat cgfOffsetMoveAmount;
  
in viewDidLoad:

  yourUITextField.delegate = self;
  yourUITextField.tag = 1;
  
in @implementation:

  - (void)setcgfOffsetMoveAmount:(NSInteger) nsiUserInTextFieldWithTag {
      if (nsiUserInTextFieldWithTag == 1) {
          cgfOffsetMoveAmount = 100;
      } else if (nsiUserInTextFieldWithTag == 1) {
          cgfOffsetMoveAmount = 200;
      } else if (nsiUserInTextFieldWithTag == 1) {
          cgfOffsetMoveAmount = 300;
      } else if (nsiUserInTextFieldWithTag == 4) {
          cgfOffsetMoveAmount = 400;
      }
  }
  
  - (void) makeKeyboardOffset
  {
      if (bIsRaised == NO)
      {
          [UIView beginAnimations:nil context:NULL];
          [UIView setAnimationDuration:0.25];
          self.view.center = CGPointMake(self.view.center.x, self.view.center.y - cgfOffsetMoveAmount);
          [UIView commitAnimations];
          bIsRaised = YES;
      } else {
          [UIView beginAnimations:nil context:NULL];
          [UIView setAnimationDuration:0.25];
          self.view.center = CGPointMake(self.view.center.x, self.view.center.y + cgfOffsetMoveAmount);
          [UIView commitAnimations];
          bIsRaised = NO;
      }
  }
  
  - (void)textFieldDidBeginEditing:(UITextField *)textField {
      [self setcgfOffsetMoveAmount:textField.tag];
      [self makeKeyboardOffset];
  }
  
  - (void)textFieldDidEndEditing:(UITextField *)textField {
      [self makeKeyboardOffset];
  }
