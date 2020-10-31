from flask import Flask, request, jsonify
from PIL import Image, ImageDraw, ImageFont
import os, time, string, os.path, sys, random
import pyrebase
import json
import requests


config = {
    "apiKey": "AIzaSyBwEfkEn_QcinWh5iGCs9pz3p6ZkhjGo-w",
    "authDomain": "fir-test-93803.firebaseapp.com",
    "databaseURL": "https://fir-test-93803.firebaseio.com",
    "projectId": "fir-test-93803",
    "storageBucket": "fir-test-93803.appspot.com",
    "messagingSenderId": "757945702647",
    "appId": "1:757945702647:web:0d51d689e57669b2779bf2",
}

# init firebase
firebase = pyrebase.initialize_app(config)
# real time database instance
db = firebase.database()
# storage Firebase
storage = firebase.storage()
# auth instance
auth = firebase.auth()


class ClasskaNam:
    useruid = None
    timestampit = None
    alllink = None

    @staticmethod
    def klasskaNam():
        allLink = (
        db.child(ClasskaNam.useruid)
        .child(ClasskaNam.timestampit)
        .shallow()
        .get()
        )
        if not os.path.exists("uploads" + "/" + ClasskaNam.useruid):
             os.mkdir("uploads" + "/" + ClasskaNam.useruid)
        os.mkdir("uploads" + "/" + ClasskaNam.useruid + "/" + ClasskaNam.timestampit)
        a = allLink.val()

        count = 0
        if (allLink.val() != None):
            for i in allLink.val():
                count += 1
                print(i)
                alll = (
                    db.child(ClasskaNam.useruid)
                    .child(ClasskaNam.timestampit)
                    .child(i)
                    .child("link")
                    .shallow()
                    .get()
                ).val()

                splitlist = alll.split("|-!-|", 1)
                if splitlist[1] == "application/octet-stream":
                    r = requests.get(splitlist[0], allow_redirects=True)
                    open("{}/{}/font{}.ttf".format("uploads" + "/" + ClasskaNam.useruid,ClasskaNam.timestampit,count), "wb").write(r.content)
                    print("FontFile")
                elif splitlist[1] == "text/plain":
                    r = requests.get(splitlist[0], allow_redirects=True)
                    open("{}/{}/text{}.txt".format("uploads" + "/" + ClasskaNam.useruid,ClasskaNam.timestampit,count), "wb").write(r.content)
                    print("TextFile")
                else:
                    print("WrongFile")


class AssignmentX:
    directoryName = None
    opacity = 255
    color1 = (0, 0, 0, 255)
    color2 = (255, 255, 255, 255)
    opage = None
    wtext = None
    sfont = None
    download = None
    @staticmethod
    def assignmentx(path, path1):

        font = list()
        if(AssignmentX.opage == None or AssignmentX.opage == "UCoE Assignment Page"):
            SheetImage = "C:/Users/dedsec995/AssigmentXApi/essentials/UCoE.jpg"
            fontsize = 75
        else:
            SheetImage = "C:/Users/dedsec995/AssigmentXApi/essentials/normal.jpeg"
            fontsize = 100

        if(AssignmentX.wtext == None or AssignmentX.wtext== ''):
            for files in os.listdir(path):    
                if files.endswith(".txt"):
                    TextFile = os.path.join(path, files)
            fileopen = open(TextFile, encoding="utf8")
            text = fileopen.read()
            fileopen.close()        
        else:
            text = AssignmentX.wtext
            print(text)


        if(AssignmentX.sfont == "No, I will use yours" or AssignmentX.sfont == None):
            font.append(ImageFont.truetype("C:/Users/dedsec995/AssigmentXApi/essentials/Utsav-1.ttf", fontsize))
            font.append(ImageFont.truetype("C:/Users/dedsec995/AssigmentXApi/essentials/Utsav-2.ttf", fontsize))
            font.append(ImageFont.truetype("C:/Users/dedsec995/AssigmentXApi/essentials/Utsav-3.ttf", fontsize))
        else:
            for files in os.listdir(path):
                if files.endswith(".ttf"):
                    font.append(ImageFont.truetype(os.path.join(path, files), fontsize))

        images = list()

        pages = 0
        boolean = 1
        # from numpy import random
        # Opening the blank page
        def type_pages(pages, text, boolean):
            
            page = Image.open(SheetImage).convert("RGBA")
            width, height = page.size
            if (AssignmentX.opage == None or AssignmentX.opage == "UCoE Assignment Page"):
                left_margin = 260 #  440
                top_margin = 230  #  325
                line_space = 67   #  96
                bottom_margin = height - 100  #height - 100
                
            else:
                left_margin = 440
                top_margin = 335
                line_space = 96
                bottom_margin = height - 300
                

            txt = Image.new("RGBA", page.size, (255, 255, 255, 0))
            draw = ImageDraw.Draw(txt)
            lwidth = 0

            for index, letter in enumerate(text):
                # if top_margin > height - 300:
                #     copy.save("{}{}.png".format(name, pages))
                #     print("PRINTED PAGE {}".format(pages + 1))
                #     pages += 1
                #     text = text[index:]
                #     type_pages(pages, text, boolean)
                #     break

                # print(top_margin, height)
                if (letter == "\n") or (lwidth >= (width - left_margin - 90)):
                    # start_index = index
                    lwidth = 0
                    top_margin += line_space
                    if top_margin > height - 300:
                        txt = Image.alpha_composite(page, txt)
                        # txt.save("{}{}.png".format("name", pages))
                        images.append(txt.convert("RGB"))
                        pages += 1
                        text = text[index:]
                        type_pages(pages, text, boolean)
                        break
                if letter == "\t":
                    lwidth += 100
                human = random.randint(0, 5)
                fonts = random.choice(font)
                add_sub = random.randint(0, 1)

                if letter == "$" and boolean == 1:
                    color = AssignmentX.color2
                    boolean = 0
                    if index == len(text) - 1:
                        # print("DONE WRITING")
                        txt = Image.alpha_composite(page, txt)
                        # txt.save("{}{}.png".format("name", pages))
                        images.append(txt.convert("RGB"))
                        images[0].save(
                            "{}.pdf".format(os.path.join(path,AssignmentX.directoryName)),
                            save_all=True,
                            append_images=images[1:],
                        )
                        storage.child("Files" + "/" + ClasskaNam.useruid + "/" + ClasskaNam.timestampit + "/" + ClasskaNam.timestampit + ".pdf").put(os.path.join(path,AssignmentX.directoryName) + ".pdf")
                        AssignmentX.download = storage.child("Files" + ClasskaNam.useruid + "/" + ClasskaNam.timestampit + "/" + ClasskaNam.timestampit + ".pdf").get_url(None)
                    else:
                        continue
                elif letter == "$" and boolean == 0:
                    color = AssignmentX.color1
                    boolean = 1
                    if index == len(text) - 1:
                        # print("DONE WRITING")
                        txt = Image.alpha_composite(page, txt)
                        # txt.save("{}{}.png".format("name", pages))
                        images.append(txt.convert("RGB"))
                        images[0].save(
                            "{}.pdf".format(os.path.join(path,AssignmentX.directoryName)),
                            save_all=True,
                            append_images=images[1:],
                        )
                        storage.child("Files" + "/" + ClasskaNam.useruid + "/" + ClasskaNam.timestampit + "/" + ClasskaNam.timestampit + ".pdf").put(os.path.join(path,AssignmentX.directoryName) + ".pdf")
                        AssignmentX.download = storage.child("Files" + ClasskaNam.useruid + "/" + ClasskaNam.timestampit + "/" + ClasskaNam.timestampit + ".pdf").get_url(None)
                    else:
                        continue
                elif boolean == 0:
                    color = AssignmentX.color2
                else:
                    color = AssignmentX.color1
                    boolean = 1

                if add_sub == 0:
                    draw.text(
                        (left_margin + lwidth, top_margin + human),
                        letter,
                        # fill=(10, 15, 85, 255),
                        fill=color,
                        font=fonts,
                    )
                else:
                    draw.text(
                        (left_margin + lwidth, top_margin - human),
                        letter,
                        # fill=(10, 15, 85, 255),
                        fill=color,
                        font=fonts,
                    )
                # txt = Image.alpha_composite(page, txt)
                lwidth += draw.textsize(letter, fonts)[0]
                # print(draw.textsize(letter, fonts)[0])
                # print(index)
                if index == len(text) - 1:
                    # print("DONE WRITING")
                    txt = Image.alpha_composite(page, txt)
                    # txt.save("{}{}.png".format("name", pages))
                    images.append(txt.convert("RGB"))
                    images[0].save(
                        "{}.pdf".format(os.path.join(path,AssignmentX.directoryName)),
                        save_all=True,
                        append_images=images[1:],
                    )
                    storage.child("Files" + "/" + ClasskaNam.useruid + "/" + ClasskaNam.timestampit + "/" + ClasskaNam.timestampit + ".pdf").put(os.path.join(path,AssignmentX.directoryName) + ".pdf")
                    AssignmentX.download = storage.child("Files" + "/" + ClasskaNam.useruid + "/" + ClasskaNam.timestampit + "/" + ClasskaNam.timestampit + ".pdf").get_url(None)
                    # exit()
            # copy.save("text{}.png".format(pages))

        type_pages(pages, text, boolean)

#Init The APPPPPPPP MERE BAppppppp
app = Flask(__name__)

# root
@app.route("/")
def index():

    return "Your Welcomed By The Greatest Luhar !!!!"

# GET
@app.route('/users/<user>')
def hello_user(user):

    return "Hello %s!" % user

# POST
@app.route('/api/assignmentx', methods=['POST'])
def GetMeAssigmentX():

    json = request.get_json()
    print(json)
    if len(json['useruid']) == 0:
        return jsonify({'error': 'invalid input'})
    ClasskaNam.useruid = json["useruid"]
    ClasskaNam.timestampit = json["timestampit"]
    ClasskaNam.klasskaNam()
    AssignmentX.directoryName= ClasskaNam.timestampit
    AssignmentX.opacity = int(json["opacity"])
    lol = json["color1"]
    h = lol.lstrip("#")
    a = tuple(int(h[i : i + 2], 16) for i in (0, 2, 4))
    a = a + (AssignmentX.opacity,)
    AssignmentX.color1 = a
    lol2 = json["color2"]
    h2 = lol2.lstrip("#")
    a2 = tuple(int(h2[i : i + 2], 16) for i in (0, 2, 4))
    a2 = a2 + (AssignmentX.opacity,)
    AssignmentX.color2 = a2
    AssignmentX.wtext = json["wtext"]
    AssignmentX.opage = json["opage"]
    AssignmentX.sfont = json["sfont"]
    AssignmentX.assignmentx("uploads" + "/" + ClasskaNam.useruid + "/" + ClasskaNam.timestampit,ClasskaNam.timestampit)
    return jsonify({"useruid": json["useruid"],"timestampit": json["timestampit"],"opacity": json["opacity"],"color1": json["color1"],"color2": json["color2"],"wtext": json["wtext"],"opage": json["opage"],"sfont": AssignmentX.download})
  
# running web app in local machine
if __name__ == '__main__':
    app.run(host='0.0.0.0', debug=True)