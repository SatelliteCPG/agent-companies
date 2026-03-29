# Email Triage Patterns

Common email types encountered by CPG brand sales teams, with classification rules and CRM action mappings.

## Email Type: Buyer Inquiry

**Signals**: New retailer buyer reaching out, questions about product line, request for information, "interested in carrying," "tell me more about"

**CRM Actions**:
- Create contact (role: BUYER) if new
- Create account if retailer is new
- Create opportunity (stage: PROSPECTING)
- Flag for immediate follow-up

**Priority**: High — respond within 24 hours

## Email Type: Broker Update

**Signals**: Weekly report from broker, store visit recap, "here's the update on," retailer feedback relay, void closure report

**CRM Actions**:
- Update existing opportunities with new information
- Create meetings if store visits are mentioned
- Update contact records if new people are referenced
- Log activity notes on relevant accounts

**Priority**: Medium — process during daily triage

## Email Type: Distributor Notification

**Signals**: UNFI or KeHE correspondence, DC authorization status, code setup confirmation, discontinuation notice, pricing update, "your item has been"

**CRM Actions**:
- Note distributor code status changes
- Update opportunity if authorization affects pipeline
- Flag discontinuation notices for immediate attention

**Priority**: High for discontinuations, Medium for routine updates

## Email Type: Sample Request Follow-up

**Signals**: "Received the samples," "samples arrived," "tried your product," "when can we get samples," "need samples for"

**CRM Actions**:
- Create sample request if new request
- Update existing sample request status
- Update opportunity stage if buyer feedback is positive
- Create follow-up meeting if evaluation timeline mentioned

**Priority**: High — samples drive conversion

## Email Type: Meeting Confirmation

**Signals**: Calendar invite, "confirming our meeting," "see you on [date]," "agenda for our call," meeting recap, "following up from our meeting"

**CRM Actions**:
- Create meeting record with date, time, attendees
- Link to relevant account and contacts
- If recap: update opportunity with discussed outcomes
- Extract action items as follow-up tasks

**Priority**: Medium — ensure CRM reflects all buyer touchpoints

## Email Type: Category Review Communication

**Signals**: "Category review," "reset window," "submission deadline," "new item form," "planogram," "schematic"

**CRM Actions**:
- Create or update opportunity (stage: CATEGORY_REVIEW)
- Note deadline dates
- Flag for buyer-meeting-brief preparation

**Priority**: High — category reviews are time-sensitive with hard deadlines

## Email Type: Promotional Communication

**Signals**: "TPR," "temporary price reduction," "ad," "endcap," "promotional pricing," "display," "feature"

**CRM Actions**:
- Update opportunity with promotion details
- Note promotional dates and pricing
- Flag if promotional pricing approval is needed

**Priority**: Medium — track but don't block on

## Classification Decision Tree

```
1. Does the email mention a specific date/time for a call or meeting?
   YES -> Meeting Confirmation (create meeting)
   NO  -> continue

2. Is the sender from a distributor (UNFI, KeHE, etc.)?
   YES -> Distributor Notification
   NO  -> continue

3. Does the email mention samples?
   YES -> Sample Request Follow-up
   NO  -> continue

4. Does the email mention category review, reset, or submission?
   YES -> Category Review Communication
   NO  -> continue

5. Is the sender a new contact inquiring about the product?
   YES -> Buyer Inquiry
   NO  -> continue

6. Is the sender a broker or partner firm?
   YES -> Broker Update
   NO  -> continue

7. Does the email mention promotions, TPR, or ads?
   YES -> Promotional Communication
   NO  -> General correspondence — log as activity note
```
