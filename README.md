# Portfolio

import pygame
pygame.init()
wn = pygame.display.set_mode((300,300))

gamestate = [
  [0,0,0],
  [0,0,0],
  [0,0,0]
]
turn = 1
gameon = True

while gameon:
  wn.fill((0,0,0))

  bd00=pygame.draw.rect(wn,(255,255,255),(2,2,96,96))
  bd01=pygame.draw.rect(wn,(255,255,255),(102,2,96,96))
  bd02=pygame.draw.rect(wn,(255,255,255),(202,2,96,96))

  bd10=pygame.draw.rect(wn,(255,255,255),(2,102,96,96))
  bd11=pygame.draw.rect(wn,(255,255,255),(102,102,96,96))
  bd12=pygame.draw.rect(wn,(255,255,255),(202,102,96,96))

  bd20=pygame.draw.rect(wn,(255,255,255),(2,202,96,96))
  bd21=pygame.draw.rect(wn,(255,255,255),(102,202,96,96))
  bd22=pygame.draw.rect(wn,(255,255,255),(202,202,96,96))

  bd = [
    [bd00,bd01,bd02],
    [bd10,bd11,bd12],
    [bd20,bd21,bd22]
  ]

  ev = pygame.event.get()
  for event in ev:
    if event.type == pygame.MOUSEBUTTONUP:
      pos = pygame.mouse.get_pos()
      for rownum in [0,1,2]:
        for colnum in [0,1,2]:
          if bd[rownum][colnum].collidepoint(pos) and gamestate[rownum][colnum] == 0:
            if turn == 1:
              gamestate[rownum][colnum] = 1
              turn = 2
            else:
              gamestate[rownum][colnum] = 2
              turn = 1


  for colnum in [0,1,2]:
    for rownum in [0,1,2]:
      square = gamestate[rownum][colnum]
      if square == 1:
        pygame.draw.circle(wn,(0,0,0),(colnum*100+50,rownum*100+50),30)
        pygame.draw.circle(wn,(255,255,255),(colnum*100+50,rownum*100+50),29)
      elif square == 2:
        pygame.draw.line(wn,(0,0,0),(colnum*100+25,rownum*100+25),(colnum*100+75,rownum*100+75))
        pygame.draw.line(wn,(0,0,0),(colnum*100+75,rownum*100+25),(colnum*100+25,rownum*100+75))

  for rownum in[0,1,2]:
    if gamestate[rownum][0] == gamestate [rownum][1] == gamestate [rownum][2] and gamestate[rownum][0] != 0:
      if gamestate[rownum][0] == 1:
        print("\n\nO has won!\n\n")
        gameon = False
      else: 
        print("\n\nX has won!\n\n")
        gameon = False

  for colnum in[0,1,2]:
    if gamestate[0][colnum] == gamestate [1][colnum] == gamestate [2][colnum] and gamestate[0][colnum] != 0:
      if gamestate[0][colnum] == 1:
        print("\n\nO has won!\n\n")
        gameon = False
      else: 
        print("\n\nX has won!\n\n")
        gameon = False
  
  if gamestate[0][0] == gamestate [1][1] == gamestate [2][2] and gamestate[0][0] != 0:
      if gamestate[0][0] == 1:
        print("\n\nO has won!\n\n")
        gameon = False
      else: 
        print("\n\nX has won!\n\n")
        gameon = False
  
  if gamestate[0][2] == gamestate [1][1] == gamestate [2][0] and gamestate[0][2] != 0:
      if gamestate[0][2] == 1:
        print("\n\nO has won!\n\n")
        gameon = False
      else: 
        print("\n\nX has won!\n\n")
        gameon = False
    
  tie = True
  if gameon == True:
    for rownum in [0,1,2]:
      for colnum in [0,1,2]:
        if gamestate[rownum][colnum] == 0:
          tie = False
    
  if tie:
    print("\n\nTie!\n\n")
    gameon = False
  
  pygame.display.update()
  
