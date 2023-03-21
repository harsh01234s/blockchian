// SPDX-License-Identifier: GPL
pragma solidity >=0.5.0 <0.9.0;

contract game {
    struct Event {
        address organizer;
        string name;
        uint data;
        uint price;
        uint ticketCount;
        uint ticketsremain;
    }

    mapping(uint => Event) public events;
    mapping(address => mapping(uint => uint)) public tickets;
    uint public nextId;

    function creatEvent(string memory name, uint data, uint price, uint ticketCount) external {
        require(data > block.timestamp, "You can only organize events for future dates");
        require(ticketCount > 0, "You can only organize events if you create more than 0 tickets");
        events[nextId] = Event(msg.sender, name, data, price, ticketCount,ticketCount);
        nextId++;
    }

    function buyticket(uint id, uint quantity) external payable {
        require(events[id].data != 0, "This event does not exist");
        require(events[id].data > block.timestamp, "Event has already occurred");
        Event storage _event = events[id];
        require(msg.value == (_event.price * quantity), "Not enough tickets");
        require(_event.ticketsremain >= quantity, "Not enough tickets");
        _event.ticketsremain -= quantity;
        tickets[msg.sender][id] += quantity;
    }

    function transferticket(uint id, uint quantity, address to) external {
        require(events[id].data != 0, "This event does not exist");
        require(events[id].data >block.timestamp, "Event has already occurred");
        require(tickets[msg.sender][id] >= quantity, "Not enough tickets");
        tickets[msg.sender][id] -= quantity;
        tickets[to][id] += quantity;
    }
}
