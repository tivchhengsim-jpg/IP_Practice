# Week 3 — Vue Components and Reactivity

## 1. In EventList, what goes wrong if you use the array index as :key and the list gets filtered while a card has local state (for example an open details panel)? 

If we use the array index as `:key` , if we remove an event then other events index will update too so Vue might reuse an EventCard component to the different event which cause local state like detail property appear on the wrong cart for example the informaton of Event 2 isplay on Panel of event 1 . 

## 2.Why is visible a computed and not a function called from the template? What is the difference when you type in the search box? 
We use `computed` because `visible` depends on reactive data such as `search`, `category`, and `events`.
The difference is that a computed property caches its result and recalculates only when its dependencies change, while a normal function called from the template runs whenever the template re-renders.When we type in the search box, `search` changes, so `visible` recalculates and automatically updates the displayed events.

## 3. EventCard emits book instead of changing event.booked. Give two reasons. 
the 2 reason are : 
1: `event` is a prop that received from the parent, so `EventCard` is the child can't  modify it directly. 
2:, `EventCard` just for handle user interaction while `App.vue` handles the booking logic and updates the event data. so emitting book separates responsibilities and orderthing also go wrong : example is eventcart increase evented.booked then `mybooking` and `bookingCount` are unchange

## 4. You write const { booked } = reactive(event); booked++. The page does not change. Why? 
if we destructure `booked` from a reactive object , that creates a separate local variable containing its value. so `booked++`, only the local variable changes, not the original reactive property. Therefore, the page doesn't change.

## 5. Where does `myBookings` live, and why not in EventCard or EventList?

`myBookings` lives in `App.vue`.
It is not in `EventCard` or `EventList` because `EventCard`responsible for displaying each event as card, while `EventList` handles searching and filtering. App have event data and handle on user booking update which is easy to update the bokkingCount also.