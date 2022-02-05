# tennis-game
a virtual tennis game 
class Game:
    def __init__(self, server, receiver):
        self.server = server
        self.receiver = receiver
        self.score = (0, 0)
        self.display = {0: "Love", 1: "15", 2: "30", 3: "40", 4: "Adv"}

    def point_to(self, player):
        if self.receiver == player:
            self.score = (self.score[0], self.score[1] + 1)
        elif self.server == player:
            self.score = (self.score[0] + 1, self.score[1])

    def get_score(self): #if scores are equal and not 40, return score all
        if self.score[0] == self.score[1]:
            if self.score[0] == 3:
                return "Deuce"
            else:
                return "{}-All".format(self.display.get(self.score[0]))
        elif set(self.score) == {0, 4}:
            return "Game Williams"
        elif set(self.score) == {3, 4}:
            player_mapping = {0: self.server, 1: self.receiver}
            player_adv = player_mapping.get(self.score.index(4))
            return "Adv {}".format(player_adv)
        else:
            return "{}-{}".format(self.display.get(self.score[0]), self.display.get(self.score[1]))

game = Game("Nadal", "Williams")
print(game.server, game.receiver)
print(game.score)
