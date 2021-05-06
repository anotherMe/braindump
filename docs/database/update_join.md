# Update with join

<code>
UPDATE vehicles_vehicle AS v 
SET price = s.price_per_vehicle
FROM shipments_shipment AS s
WHERE v.shipment_id = s.id 
</code>