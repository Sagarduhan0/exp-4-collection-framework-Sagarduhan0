import java.util.LinkedList;
import java.util.Queue;
import java.util.concurrent.locks.Lock;
import java.util.concurrent.locks.ReentrantLock;

class TicketBooking {
    private final boolean[] seats; 
    private final Lock lock = new ReentrantLock(); 

    public TicketBooking(int totalSeats) {
        seats = new boolean[totalSeats]; 
    }

    public void bookSeat(int seatNumber) throws Exception {
        lock.lock(); 
        try {
            if (seatNumber < 0 || seatNumber >= seats.length) {
                throw new Exception("Invalid seat number.");
            }
            if (seats[seatNumber]) {
                throw new Exception("Seat " + seatNumber + " already booked.");
            }
            seats[seatNumber] = true; 
            System.out.println("Seat " + seatNumber + " booked successfully.");
        } finally {
            lock.unlock(); 
        }
    }
}

class BookingRequest implements Runnable {
    private final TicketBooking ticketBooking;
    private final int seatNumber;

    public BookingRequest(TicketBooking ticketBooking, int seatNumber) {
        this.ticketBooking = ticketBooking;
        this.seatNumber = seatNumber;
    }

    @Override
    public void run() {
        try {
            ticketBooking.bookSeat(seatNumber);
        } catch (Exception e) {
            System.out.println(e.getMessage());
        }
    }
}

public class TicketBookingSystem {
    public static void main(String[] args) {
        TicketBooking ticketBooking = new TicketBooking(10); 
        Queue<Thread> bookingQueue = new LinkedList<>();

        for (int i = 0; i < 5; i++) {
            Thread vipBooking = new Thread(new BookingRequest(ticketBooking, i));
            vipBooking.setPriority(Thread.MAX_PRIORITY); 
            bookingQueue.add(vipBooking);
        }

        for (int i = 5; i < 10; i++) {
            Thread regularBooking = new Thread(new BookingRequest(ticketBooking, i));
            regularBooking.setPriority(Thread.NORM_PRIORITY); 
            bookingQueue.add(regularBooking);
        }

        while (!bookingQueue.isEmpty()) {
            Thread bookingThread = bookingQueue.poll();
            if (bookingThread != null) {
                bookingThread.start(); 
                try {
                    bookingThread.join();
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
        }
    }
}
