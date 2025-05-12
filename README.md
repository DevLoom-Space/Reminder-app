# Reminder-app


from tabulate import tabulate


class Reminder:
  def __init__(self, title, time):
    self.title = title
    self.time = time
    self.done = False
  
  def mark_done(self):
    self.done = True
    
reminders_dict = {}
  


      


def add_reminder():
  global reminders_dict
  
  print("\n----Add New Reminder ----")
  title = input("Enter the Title of your reminder: ")
  time =  input("Enter the time of your reminder: ")
  
  next_id = len(reminders_dict) + 1
  new_reminder = Reminder(title, time)
  
  reminders_dict[next_id] = new_reminder
  print(f"Reminder '{title}' added with ID {next_id}! ")
  
  
  
def view_reminder():
    if not reminders_dict:
      print("\n No reminders yet. ")
      return
    
    reminders_table = []
    
    for reminder_id, reminder in reminders_dict.items():
      status = "Done" if reminder.done else 'Not Done'
      reminders_table.append([reminder_id, reminder.title,reminder.time, status])
      
      
    print("\n----Your Reminders----")
    print(tabulate(reminders_table, headers=["ID", "Title","Time","Status"], tablefmt="grid"))
      
def mark_done():
  if not reminders_dict:
    print("\n No Reminders to mark.Add some first")
    return
  
  
  try:
    
    done_id = int(input("Enter the ID of the Reminder you want to mark as done: "))
    if done_id in reminders_dict:
      
      reminders_dict[done_id].mark_done()
      print(f"Reminder '{reminders_dict[done_id].title}' marked as done")
    
    else:
      print("That Id does not exist.")
   
  except ValueError:
    print("Enter a valid Number.")
    
    
    
    
def delete_reminder():
  if not reminders_dict:
    print("\nNo Reminders to delete")    
    return
  
  try:
    
    del_id = int(input("Enter the ID of the Reminder to delete: "))
    if del_id in reminders_dict:
      deleted_title = reminders_dict[del_id].title
      del reminders_dict[del_id]
      print(f"Reminder '{deleted_title}', deleted.")
      
    else:
      print("That ID does not exist")
      
  except ValueError:
    print("Please enter a valid number.")    
    
    
    
def main_menu():
  while True:
    print("\nWhat would you like to do")
    print("1. Add Reminder")
    print("2. View Reminders")  
    print("3. Mark Reminder as Done")
    print("4. Delete Reminder")
    print("5. Exit")
    
    choice = input("Enter your choice: ").strip()
    
    if choice == "1":
      add_reminder()
    
    elif choice == "2":
      view_reminder()
      
    elif choice == "3":
      mark_done()
      
    elif choice =="4":
      delete_reminder()
      
    elif choice =="5":
      print("Goodbye!")
      break
    
    else:
      print("Invalid choice. Try again")
      
    
    
main_menu()
      
            
 
      