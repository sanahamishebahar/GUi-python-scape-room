# GUi-python-scape-room

import tkinter as tk
import random


window = tk.Tk()
window.title("Mystery Room")
window.geometry("550x450")


# اطلاعات بازی
room = 1
life = 3
score = 0


# ---------------- صفحه شروع ----------------

start_frame = tk.Frame(window)

start_frame.pack(fill="both", expand=True)


title = tk.Label(
    start_frame,
    text="🗝️ MYSTERY ROOM 🗝️",
    font=("Arial", 28, "bold"),
    fg= "blue"
)

title.pack(pady=40)


story = tk.Label(
    start_frame,
    text="You are trapped in a mysterious castle.\n"
         "Choose the correct doors and escape!",
    font=("Arial", 14),
    fg= "blue"
)

story.pack()


def start_game():

  global room, life, score

  room = 1
    life = 3
    score = 0

  start_frame.pack_forget()
    game_frame.pack(fill="both", expand=True)

show_room()



start_button = tk.Button(
    start_frame,
    text="START GAME",
    font=("Arial", 16),
    width=15,
    fg = "red",
    bg = "lightblue",
    command=start_game
)

start_button.pack(pady=40)



# ---------------- صفحه بازی ----------------


game_frame = tk.Frame(window)



info_label = tk.Label(
    game_frame,
    font=("Arial", 14)
)

info_label.pack(pady=10)



room_label = tk.Label(
    game_frame,
    font=("Arial", 20)
)

room_label.pack(pady=20)



message = tk.Label(
    game_frame,
    font=("Arial", 13),
    wraplength=400
)

message.pack()



# انتخاب در


def choose_door(number):

  global room, life, score


  wrong_door = random.randint(1,3)


    
  if number == wrong_door:


   life -= 1

   if life == 0:

   game_over()

  else:

   message.config(
                text=f"💀 Wrong door!\nYou lost a life.\n❤️ Life: {life}"
            )



   else:


  score += 10


  events = [
            "🔑 You found an ancient key!",
            "💎 You discovered a hidden treasure!",
            "🗺️ You found a secret map!",
            "✨ A magic door appeared!"
        ]


   message.config(
            text=random.choice(events)
        )


   room += 1



   if room > 5:

  win_game()

  else:

   window.after(1500, show_room)




def show_room():


  info_label.config(
        text=f"❤️ Life: {life}        ⭐ Score: {score}"
    )


  room_label.config(
        text=f"🏰 Room {room}\nChoose a door"
    )


  door1.pack(pady=5)
    door2.pack(pady=5)
    door3.pack(pady=5)



def hide_doors():

   door1.pack_forget()
    door2.pack_forget()
    door3.pack_forget()



def game_over():

   room_label.config(
        text="💀 GAME OVER 💀"
    )

  message.config(
        text=f"You died!\nFinal Score: {score}"
    )

   hide_doors()

   restart_button.pack(pady=20)



def win_game():

   room_label.config(
        text="🏆 YOU ESCAPED!"
    )

  message.config(
        text=f"Congratulations!\nScore: {score}"
    )

  hide_doors()

   restart_button.pack(pady=20)



def restart():

   game_frame.pack_forget()
    restart_button.pack_forget()
    start_frame.pack(fill="both", expand=True)



# دکمه های در


door1 = tk.Button(
    game_frame,
    text="🚪 Door 1",
    width=20,
    command=lambda: choose_door(1)
)


door2 = tk.Button(
    game_frame,
    text="🚪 Door 2",
    width=20,
    command=lambda: choose_door(2)
)


door3 = tk.Button(
    game_frame,
    text="🚪 Door 3",
    width=20,
    command=lambda: choose_door(3)
)



restart_button = tk.Button(
    game_frame,
    text="Restart",
    command=restart
)



window.mainloop()
