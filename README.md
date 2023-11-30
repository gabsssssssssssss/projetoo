import chess
import chess.svg
import chess.engine
import random

def jogada_aleatoria(tabuleiro):
    movimentos = list(tabuleiro.legal_moves)
    return random.choice(movimentos)

def jogada_ia_stockfish(tabuleiro):
    with chess.engine.SimpleEngine.popen_uci("C:/caminho/para/stockfish.exe") as engine:
        result = engine.play(tabuleiro, chess.engine.Limit(time=2.0))
        return result.move

def jogar():
    tabuleiro = chess.Board()

    while not tabuleiro.is_game_over():
        print(tabuleiro)
        if tabuleiro.turn == chess.WHITE:
            jogada = input("Digite sua jogada: ")
            tabuleiro.push(chess.Move.from_uci(jogada))
        else:
            # Substitua pela sua IA usando Stockfish
            jogada_ia = jogada_ia_stockfish(tabuleiro)
            tabuleiro.push(jogada_ia)

    print("Fim de jogo!")
    print("Resultado: " + tabuleiro.result())

if __name__ == "__main__":
    jogar()
