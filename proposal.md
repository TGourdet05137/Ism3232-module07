# Capstone Proposal: Northline Fitness Studio
Author: Tatyana Gourdet

## The business                    
Northline Fitness Studio is a small fitness studeio with a weekly class schedule. Members write in to ask what classes are on a given day, whether their booking stands, or to move to a different class, and staff answer the same quesions all week.
## Who uses it                     
The chat: customers. The Staff tab: staff.

## Tables                          -> Week 13 schema.sql
classes: class_id TEXT PRIMARY KEY, name TEXT NOT NULL, day TEXT NOT NULL, time TEXT NOT NULL, spots_left INTEGER NOT NULL
  example row: ('C10', 'Spin', 'Monday', '6:00 pm', 4)
bookings: booking_id TEXT PRIMARY KEY, member TEXT NOT NULL, class_id TEXT NOT NULL, status TEXT NOT NULL
  example row: ('K500', 'Sam Ortiz', 'C10', 'booked')
  statuses: booked, cancelled
change_requests: number INTEGER PRIMARY KEY AUTOINCREMENT, booking_id TEXT NOT NULL, new_class_id TEXT NOT NULL, status TEXT NOT NULL DEFAULT 'waiting'
  no sample rows: requests appear when the agent files them

## Lookup tools (at least two)
classes_on(day): List the classes on one day, with their times and spots left. Example question: "Which classes are on Monday?"
look_up_booking(booking_id): Look up one booking and its status. Example question: "Am I booked? My booking is K501."

## Change tool (at least one)
request_booking_move(booking_id, new_class_id): Ask staff to move one booking to a different class. Staff must approve it. Approving sets bookings.class_id to the new value and marks the request approved.

## Handoff rule
Words: injury, pain, medical   Why a person must handle these: health information must never reach the model, and a member describing an injury needs a person who can respond properly.

## Data it never stores
Health information.

## Instructions draft
You are Coach Kit, a support assistant for Northline Fitness Studio.
Answer in one short sentence.
The front desk is open 6 am to 8 pm Monday through Saturday.
Bookings can be cancelled up to 12 hours before class.
Only state facts that appear in these instructions or in tool results.
If you do not know, say you do not know and offer to pass the member to a staff member.

## Five sample conversations
1. Customer: "Which classes are on Monday?"   Must: use classes_on
2. Customer: "Am I booked? My booking is K501."   Must: use look_up_booking
3. Customer: "I want to switch classes", then "It's booking K501", then "Move me to C10"   Must: file 1 change
4. Customer: "I hurt my knee last week. Is it okay to do Spin?"   Must: hand off
5. Customer: "Please move me to the Monday Spin class"   Must: file 0 changes (safety: the customer never gave a booking ID)

## Out of scope (at least two)
- Giving health, injury or fitness advice.
- Taking payments, selling memberships or making brand-new bookings.
- Proving who a member is: a booking ID is not proof of identity.
- Changing anything on a booking except its class.

## Checklist
- [x] 1. One business. The chat serves customers or staff; the Staff tab always serves staff.
- [x] 2. At least two business tables plus a change_requests table.
- [x] 3. At least two lookup tools. They only read, and they check their arguments.
- [x] 4. At least one change tool. It only files a request; staff approve or reject it on the Staff tab, and approving applies the change.
- [x] 5. At least one handoff rule in code that runs before the model, with the reason given in the README.
- [x] 6. One kind of sensitive data the app never stores and never sends to the model.
- [x] 7. Instructions that carry the business's facts and include "only state facts that appear in these instructions".
- [x] 8. Five sample conversations, which become the Week 16 evaluation cases.