import java.util.*;

public class CardCollectionApp {

    static class Card {
        private String symbol;
        private String value;  

        public Card(String symbol, String value) {
            this.symbol = symbol;
            this.value = value;
        }

        public String getSymbol() {
            return symbol;
        }

        public String getValue() {
            return value;
        }

        @Override
        public String toString() {
            return value + " of " + symbol;
        }
    }

    static class CardCollection {
        private Map<String, List<Card>> cardMap;

        public CardCollection() {
            cardMap = new HashMap<>();
        }

        public void addCard(Card card) {
            cardMap.computeIfAbsent(card.getSymbol(), k -> new ArrayList<>()).add(card);
        }

        public List<Card> findCardsBySymbol(String symbol) {
            return cardMap.getOrDefault(symbol, Collections.emptyList());
        }

        public void displayAllCards() {
            for (Map.Entry<String, List<Card>> entry : cardMap.entrySet()) {
                System.out.println("Symbol: " + entry.getKey());
                for (Card card : entry.getValue()) {
                    System.out.println("  " + card);
                }
            }
        }
    }

    public static void main(String[] args) {
        CardCollection cardCollection = new CardCollection();

        cardCollection.addCard(new Card("Hearts", "A"));
        cardCollection.addCard(new Card("Hearts", "K"));
        cardCollection.addCard(new Card("Diamonds", "Q"));
        cardCollection.addCard(new Card("Clubs", "10"));
        cardCollection.addCard(new Card("Spades", "2"));
        cardCollection.addCard(new Card("Hearts", "5"));

        System.out.println("All Cards in Collection:");
        cardCollection.displayAllCards();

        Scanner scanner = new Scanner(System.in);
        System.out.print("Enter a symbol to find cards (Hearts, Diamonds, Clubs, Spades): ");
        String symbol = scanner.nextLine();

        List<Card> foundCards = cardCollection.findCardsBySymbol(symbol);
        if (foundCards.isEmpty()) {
            System.out.println("No cards found for symbol: " + symbol);
        } else {
            System.out.println("Cards found for symbol " + symbol + ":");
            for (Card card : foundCards) {
                System.out.println("  " + card);
            }
        }

        scanner.close();
    }
}
